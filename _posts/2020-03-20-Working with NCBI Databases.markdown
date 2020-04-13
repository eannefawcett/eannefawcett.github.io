---
layout: post
title:  "Working with NCBI Databases"
date:   2020-03-20 22:14:36
categories: technical, data science
paginator: Working with NCBI Databases
---
# Updates

In Biopython there are various options with which to work with genetic information.
This post will discuss integrating the API call functionality of the online
BLAST + database with an email and tool that is registered with NCBI using
the Enterz library to obtain sequence information from registered accession numbers.
The applications of this type of approach would be to compare genetic information
across broad categories, not to identify a sequenced genetic sequence or protein.

First, register your email and project tool with NCBI. This can be done by
emailing their office at 	eutilities@ncbi.nlm.nih.gov with the following information:
- email
- tool.
Your email should be the email with which you are accessing the database. All
communications about your project should go through this email. The tool is something
that you make up, a project name, something that uniquely identifies what you are
working on. NCBI will use both pieces of information to track your data usage
while you are accessing the database.
Do not access the database before receiving a confirmation email from NCBI that
you are registered for use.

Second, while you are waiting to hear back, you can register for an API key after
creating an NCBI account. This API key will allow you to access the faster.

Third, follow instructions about database usage so as to be courteous to all who
are accessing the database. NCBI has posted some rules about usage, along with
explaining them in the confirmation email that your email and tool has been registered.
For people not actively working in the research field of genomics, access the database
between the hours of 9pm EST to 6am EST. Batch your requests for unique identifiers
in batch sizes up to two hundred. Without an API key, you may contact the database
up to three times per second. With an API key, you many contact the database up
to ten times per second.

I've included a code snippet showing how to set this up for multiple batches,
with an API key.

```

def get_ncbi_data(api, email, tool, database, ids):

    """To get data from the ncbi blast data base given:
    an API key,
    an email, must be on file with ncbi,
    a tool, must be on file with ncbi,
    the database name to search, and
    the ids to search by in list format."""

    from Bio import Entrez

    import time

    Entrez.api_key = api

    Entrez.email = email

    Entrez.tool = tool

    print('Searching')

    time.sleep(10)

    search_results = Entrez.read(Entrez.epost(database, id=",".join(ids)))

    time.sleep(1)

    webenv = search_results["WebEnv"]

    query_key = search_results["QueryKey"]

    print('Fetching Results')

    results = Entrez.read(Entrez.efetch(db=database, webenv=webenv, query_key=query_key, retmode='xml'))

    ```
