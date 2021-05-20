# An alternative way to describe a IALA's G1128 service specification 

You can collaborate on the service-specification.md file for the specification then the repository will turn the file into a nicely-formatted pdf for you.

The document template is following the [IALA's G1128 service specification format](https://www.iala-aism.org/product/g1128-specification-e-navigation-technical-services/).

## Versioning of the document

A version is formatted as:
```
format: "${major}.${minor}.${patch}"
```

A commit without a reserved word only impacts to the patch element, i.e., the increament of the last element (patch version) of a version is executed whenever you make a commit.

For updating the minor element, put *(MINOR)* at the end of a commit message.

As well as the minor element, put *(MAJOR)* at the end of a commit message for major versioning updates.

You can read more details about the versioning from [Git-based symantic versioning](https://github.com/PaulHatch/semantic-version) which is used in the GitHub action of this repository.

