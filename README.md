
# Overview

In the course of this semester the war in Ukraine has changed my
perception on fossil-fuels and how we as society are dependent from it.
For the transition of all economies from a fossil-fuel-based economy to
an renewable-energy based economy, it is my opinion, mobility is one of
the most controvesial discussed and important topics. From the technical
point of view, electric engines are efficient, and using electricity
means that renewable energies can also be used. Electric mobility is for
that reason, a key technology for more sustainable mobility and is one
way of achieving ambitious energy and climate policy goals. Everything
sounds amazing and fun, but, the central question when buying an
electric vehicle (at least for me) are:

- Who are the best operators?
- Which city/region is best for electric vehicle users
- Are there any restrictions in terms of pluging devices depending on
  which city/canton?
- Do I still need special accessories, depending on the charging
  stations?

This question are answered using two APIs, a MongoDB database and graphs
in order to vizualize the data. The used API is based on the page
[`recharge-my-car.ch`](https://opendata.swiss/de/dataset/ladestationen-fuer-elektroautos/resource/e33957be-180a-422b-90a5-fbfe9774927a)
and is the face of the **National Data Infrastructure For
Electromobility (DIEMO)** and shows where charging points for electric
vehicles are and provides specific detailed information, everything
available in real time.

<br> <br>

![](final_delivery/sfoe.jpeg)

<br> <br>

**At this point it should be mentioned, that not all operators are
registered in this database.**

The correct assignment of postal codes and cities has proven to be
extremely difficult, since a city can have several postal codes and
several municipalities can share one postal code. At the same time, the
naming of the city is not consistance as well. To reduce the assignment
of cities to a single number, a second API was needed, directly from the
Swiss Post. Using this second database, the entries of the DIEMO
database were cleaned and enriched.

Last but not least, the MongoDB database is hosted on MongoDB Atlas and
available via URL.

## Document Structure: DIEMO API

The documents returned by the SFOE API were converted to JSON format and
straight away imported into their respective collection in the SFOE
database (`ChargingStations` collection). The class diagram below
represents what a *single document* looks like. However, all collections
have the same structure.

The size of all arrays **EVSEDataRecord** is the number of charging
stations accross Switzerland. The array **EVSEDataRecord** contains
further sub-arrays with the relevant information of each charging
station. The ‘{}’ indicates a nested substructure where the additional
data is found linked below the main document. Other fields have not been
presented in a separate entity in the diagramm.

<br>

![](final_delivery/UML_diagramm.png)

<br>

- The collection **ChargingStations** contains the fields
  **OperatorID**, **OperatorName** and **EVSEDataRecord**.  
- The **EVSEDataRecord** itself contains for each charging station a
  separate array containing the **Address**.
  - Within **Address** there are several sub-fields, the most important
    one is the **Address** array, which contains the details, such as
    City, Street, StreetNumber, PostalCode etc., of each charging
    station.

## Report and Code

[**Link to the
documentation**](final_delivery/Personal%20Project%20Bernardo%20Freire.pdf)
