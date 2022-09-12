# Which data storage options are suitable for the project?

Contributor(s): Syakyr Surani

There are many data storage options that one can implement for their
project, but to choose one (or several) of these options can be 
confusing to some. This guide hopes to give you some guidance in 
navigating various data storage options that are suitable for your
project by honing in on three main considerations when choosing the 
right options for you.

## Requirements and Competency of Project Sponsor

Data competency of the Project Sponsor cannot be understated when 
choosing a suitable data storage option, especially when they are not 
prepped up to be part of an AI-powered project. The skillsets of 
analysts in any given organisation can vary a lot from simple Excel 
data entry ones to highly automated processes employed by big tech 
companies. Therefore, it is important to understand the competency as 
well as the readiness of the Project Sponsor in committing on a set of 
data storage options. You can read more about this in our 
[AI Readiness Index][airi] article as one of the ways to ascertain the 
Project Sponsor's data competency.

To give an example, you have a team from the Project sponsor that has 
only started going through AI tutorials, whether from YouTube or a 
reputable course provider. The data you need for the project is 
relatively small and only require the basic skills needed to build a 
model and to be used internally and sparingly. Then, using CSV or Excel 
files may be sufficient for the project.

On the other hand, if the project takes in a lot of data from multiple
data sources, then they may want to implement a data lake to store 
those data before being processed and transformed into data 
warehouse(s). An article from Guru99 gives more insight regarding about 
data lakes and warehouses [here][lake-house].

We would also need to take the willingness of the Project Sponsor to 
accept a solution that is outside their comfort zone into consideration
as well. In some cases, they might request something that is more
sustainable than their current solution, while other Project Sponsors
may not be ready to handle databases and are only comfortable with what
they have been doing.

## Reliability and Consistency

Reliability and consistency may be important in your project, 
especially when the latest dataset may be needed to reduce model 
drifting or other similar issues. Flat files such as CSV and Excel 
files may not be a viable solution as different members in your team 
may be using different versions of data, which may result in unreliable 
and inconsistent metrics when it comes to evaluation. 

Therefore, it would be recommended to look at a more reliable solution 
such as database management systems (examples include SQL, MongoDB, 
etc.) if that is to be the case. A section provided by Microsoft Azure 
can give more information regarding these types of systems 
[here][data-store], relational or non-relational.

## Data Management (Simplicity vs Complexity)

The topic of data management coincides with the competency of your team
as well as how reliable you need the data to be in the manner of cost
efficiency. This cost could be in financial terms, in terms of your 
team's valuable time to pick up a new skillset, in terms of 
potential security and privacy issues surrounding the use of 
self-hosted or managed cloud solutions, or a mixture of all three. 

Does your organisation have the capability to resolve operational 
issues to any data store solutions proposed? Is the data sensitive 
enough to warrant an in-house solution, or is it more cost-effective to
have it run in one of the many managed cloud providers instead? Or is 
it less hassle to just share flat files such as CSV and Excel files in 
a cloud storage? These questions could be used to shape your current 
project's requirements, but you should also project those requirements 
towards the long term, and discuss within your team to reduce the times
needed to refactor your project.

## Final Thoughts

There are more considerations you may need to take note of other than
the three that is discussed in this guide, but we believe that these 
three are the main considerations to take note of. However, if you feel
that you need more tips on navigating your way on finding a suitable
data storage solution, there is a Microsoft Azure page you might find
more insights [here][criteria].

## References

- [AI Readiness Index | AI Singapore][airi]
- [Data Lake vs Data Warehouse: What's the Difference? | Guru99][lake-house]
- [Understanding Data Store Models | Microsoft][data-store]
- [Criteria for Choosing a Data Store | Microsoft][criteria]

[airi]: https://aisingapore.org/airi/
[lake-house]: https://www.guru99.com/data-lake-vs-data-warehouse.html
[data-store]: https://docs.microsoft.com/en-sg/azure/architecture/guide/technology-choices/data-store-overview
[criteria]: https://docs.microsoft.com/en-sg/azure/architecture/guide/technology-choices/data-store-considerations
