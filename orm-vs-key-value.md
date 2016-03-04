---
layout: page
title: 'Enterprise Apps: ORM vs Key-Value Storage Model'
date: 2015-01-20
---

([original gist](https://gist.github.com/unframework/a9e6b2ef47ec25f0b692))

Enterprise software models the real world of human activity, interaction, business transactions. Let's consider a typical person modeled by a run-of-the-mill e-commerce app. They'll have a few attributes (read: DB table columns):

- first, last name
- authentication credentials
- shipping address
- payment info (PayPal/Stripe token, billing address, etc)
- avatar picture
- email notification preferences
- fave PANTONE® shade (18-1438 aka Marsala?)

Ye olde ORM "model class":

```java
class Person {
  int getId(); // no setter, because why the eff would the ID change?
  String getFirstName();
  void setFirstName(String firstName);
  String getLastName();
  // etc, etc, for another 25 excruciating screen-scrolls
}
```

Note that all of it is independent data. Changing the avatar picture has zero to do with shipping address validation; first/last names are relevant to payment and delivery, but not at all to someone's notification preferences.

So why do we model it as one object? Objects are tightly grouped black boxes of state. The above ain't it.

A radically different approach is just to use key-value maps.

```java
Map<PersonId, PaymentInfo> paymentInfoByPersonId = somehowInjectedDatabaseBackedMap;
Map<PersonId, ImageAsset> avatarPictureByPersonId = somehowInjectedDatabaseBackedMap;
Map<PersonId, StreetAddress> shippingAddressByPersonId = somehowInjectedDatabaseBackedMap;
// etcetera
```

A more mainstream form (implemented in https://github.com/fxrm/fxrm-store-java and https://github.com/fxrm/fxrm-store) looks as follows:

```java
public interface ApplicationStore {
  Address getShippingAddress(PersonId pid);
  void setShippingAddress(PersonId pid, Address value);
  // etcetera
}
```

The latter approach is actually very similar to the well-known DAL pattern. The only difference is that DAL code will typically return an all-encompassing mega-class containing *all* business entity data, where our dictionary-ish approach truly splits it up into [business primitives](http://codebetter.com/drusellers/2010/01/27/business-primitives-1-2/). I'd argue that the old way of returning all data at once is almost a premature optimization (and full DB rows can still be cached in dictionary-like implementations).

Does this mean the data should be actually housed in a simple key-value store (like SimpleDB)? Absolutely not (unless it makes sense for a given app). **The above is just an abstraction layer for an underlying relational (SQL) or document data store.** It is a facade to pass to the business logic layer, but we can still use relational features in other parts of the code. Underneath, one can still manage strict schema using migrations, optimize using indexes and use joins and views to get data out in bulk for presentation/reporting. But the actual service code can be insulated from implementation details through the above dictionary metaphor.

We have successfully used this methodology in production on top of MySQL; it works! Makes unit testing a breeze and eliminates a whole class of ORM bugs. Most importantly, **it just makes human sense**. And that's a starting point to a lot of good software design.
