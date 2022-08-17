<!--
 Copyright (C) 2022 Code for Vegas Foundation
 
 This file is part of ov-open-data-capture-platform.
 
 ov-open-data-capture-platform is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.
 
 ov-open-data-capture-platform is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 
 You should have received a copy of the GNU General Public License
 along with ov-open-data-capture-platform.  If not, see <http://www.gnu.org/licenses/>.
-->

# Open Data Capture Platform Overview

The goal of this project is to enable the capture and update of city scale Open Data.

Open Data should be captured and stored in meaningfully-segregated tables, using geographical information systems (GIS) best practices wherever possible, or enabling equivalent best practice access and maniupulation.

## Project Policies

Unless otherwise and specifically indicated with replacement files in this repository, this project will adhere to the default Code for Vegas Foundation policies for Code of Conduct and Contributing, found at

* [Code of Conduct - Code for Vegas Foundation](https://github.com/CodeForVegas/.github/blob/main/CODE_OF_CONDUCT.md)
* [Contributing to this Project - Code for Vegas Foundation](https://github.com/CodeForVegas/.github/blob/main/CONTRIBUTING.md)

## General Focus Areas

This is a large and ongoing project with multiple components. Each focus area will likely require at least one component, which may be code found in github, or which may be some other component found elsewhere but tracked in github either directly or indirectly. Examples of these latter components include visual layout, icons and logos and other creative assets, videos and other larger creative assets, and so on.

### Database

The ODCP will rely heavily on an authoritative data store, most likely PostgreSQL with PostGIS extensions, along with any other extensions and auxiliary code to manage location, data privacy, data governance, etc.

It is possible that additional database(s) might be used to manage media (photos, video content, etc) and storage of that media, textual assets and translations, and so on. Here the right tool for the job should always be a primary consideration.

### Extract-Transform-Load

There is an existing bolus of City of Las Vegas Open Data available for public consumption via two ArcGIS portals (and a specific LVMPD open data portal):

[City of Las Vegas Open Data Portal](https://opendataportal-lasvegas.opendata.arcgis.com/)

[City of Las Vegas GeoCommons](https://geocommons-lasvegas.opendata.arcgis.com/)

[LVMDP Open Data Portal](https://opendata-lvmpd.hub.arcgis.com/)

Also linked in the *References* section below with policy, governance, and architectural information. These are initial conditions for this ODCP project.

In order to make use of the existing data sets, the ETL component will do exactly the three steps stated.

1. Extract data from the existing data sets. This may include cross-referencing data by row IDs as some data elements found in KML output are not found in CSV output, per data set, as an example. Placemark Geometry is one example found, surely there are a few.
2. Transform data into the form we will store in the ODCP database(s). This will likely include coalescing data from different output formats into corrected input data, and then preparing that data appropriate for destination tables (eg a standard table and a PostGIS table, data across a user and dataset schema pair, etc).
3. Load the final data into the ODCP database(s).

There is useful information to be found in the context of Open Data, at the [Socrata archicture document page](https://open-source.socrata.com/architecture/) also linked in the *References* section below. SODA should be considered during the ETL process.

### Dashboards and Visualizations

There are a variety of online resources (including at the hosting arcgis website) to enable a consumer of Open Data to locate, filter, and download or access Open Data datasets.

ArcGIS provides some basic tools to construct and display dashboards based on portal data. These are great examples, but may be considered starting points in some cases. Geospatial data is particularly interesting for visualization on 2- and 3-dimensional maps as static data, but could also be displayed as geospatial and temporal data in animated form.

Similarly, numerical and tabulated data can be displayed where appropriate as time series data, with 2- and 3-dimensional charts, interlinked tables, and whatever else might be conceived.

### Data Access APIs

There is an existing scheme in place, the Socrata Open Data API (SODA), linked below in the *References* section. This is a baseline for implementation.

Modern data may also be accessed using several commonly-used schemes which should be considered for implementation. These include at least

* RESTful APIs
* GraphQL APIs
* gRPC APIs
* Socrata APIS (SODA, SoQL)
* Other

In order to make the most of automation and implicit documentation, APIs should make maximal use of [OpenAPI tools and techniques](https://www.openapis.org/).

Access to the ODCP database(s) through public-facing APIs will take place via business logic which will take advantage of OpenAPI automation methods to generate that business logic.

### Stable and Real-Time Data

Grossly speaking, there are two types of Open Data to consider and capture:

* Stable Data - changes slowly, if at all, over relatively long time intervals.
* Real Time Data - changes quickly, possibly on time intervals measured in minutes or seconds.

Taking a practical public transit example scenario:

* Bus stop locations are very stable, in that they will change slowly and require relocation of signage and other phyiscal elements.
* Temporary bus stop locations are less stable, changing to accommodate construction, event traffic re-routing, etc and may change over the course of a day or days.
* Bus routes and schedules tend to be fairly stable but may change for special events or other adjustments.
* Bus locations vary in real time as vehicles move from stop to stop along a route according to a schedule.

By capturing these different types of data and exposing them to consumers, it is possible to build practical applications for end users that make use of open data in creative ways, without resorting to closed data siloes.

### Example Uses

Development of example applications, visualizations, and manipuations using a variety of means will help the casual user understand the scope and grandeur of city scale open data.

Some example examples:

* Jupyter Notebooks demonstrating coded data access and analysis
* Mobile/Web applications demonstrating visualization of data in practical use scenarios
* Mobile/Web applications designed to capture new information, attributed to a particular user (person)
* Embeddable widgets encapsulating a particular visualization (eg a litter map for embedding in a news article)

Ideally there will be countless examples developed over time, to enable countless applications and as important, extended broad base participation in the capture and use of Open Data!

## Tools and Methods

Beyond suggestions already stated above, the right tool for the job and best practices methodology are recommended across the entire ODCP project.

## References

[NGAC Local Gov GIS Best Practices from 2011](https://www.fgdc.gov/ngac/ngac-local-gov-gis-best-practices-paper.pdf)

[Open Data Guide for City of Las Vegas](https://files.lasvegasnevada.gov/open-data/Open_Data_Guide_for_CLV__ODSC_Approved_.pdf)

[City of Las Vegas Open Data Portal](https://opendataportal-lasvegas.opendata.arcgis.com/)

[City of Las Vegas GeoCommons](https://geocommons-lasvegas.opendata.arcgis.com/)

[City of Las Vegas Transparency in Government](https://www.lasvegasnevada.gov/Government/Transparency)

[LVMPD Open Data Portal](https://opendata-lvmpd.hub.arcgis.com/)

[Socrata Open Data API (SODA)](https://dev.socrata.com/)

[SODA Architecture](https://open-source.socrata.com/architecture/)

[Open Data Network](https://www.opendatanetwork.com/)
