code: introduction
title: Introduction
--- |

    One of the most common way of arranging data is tabular format. Be it Spreadsheets (e.g. Microsoft Excel, Google Spreadsheet, Apple Numbers etc) or RDBMS tables, we often work with data in the form of a table. It's no surprise that exploratory data analysis tools also model dataset in tabular format. Be it `R`, `Pandas` or new languages like `Julia`, they all have a data structure called `DataFrame` which is essentially an equivalent of Spreadsheet or RDBMS table.

    Of course, Spreadsheets and RDBMS tables are completely different in terms of data constraints, the kind of operations you can perform and how you perform those operations. RDBMS table constraints and functionality are designed to ensure ACID (Atomicity, Consistency, Isolation and Durability) properties across all CRUD (Create, Read, Update and Delete) operations. Spreadsheets are designed to be a fluid environment where different blocks of the same spreadsheets could perform very differently.

    In the same way, `DataFrame` is a completely different type of table in terms of how it arranges the data, the kind of operations it supports and how those operations are performed. `DataFrame` is designed for the purpose of exploratory data analysis on various kinds of datasets. The datasets tend to fit in memory, data tends to be messy and shape of the data needs to be changed very often.

    To be proficient with Spreadsheets or RDBMS, we need to not only learn the syntax of operations but also a whole different way of thinking. The mental model for manipulating a Spreadsheet is very different from an RDBMS table. It feels like programming but the language is very different.

    Similarly, to be proficient with `DataFrame`, we need to learn a different way of thinking. It's still a table like structure but that's where the similarities end. While the `DataFrame` constructs in all languages (Python/Pandas, R, Julia etc) have similarities, there are quite a few differences as well. For the purpose of this discussion, we'll use `Pandas` implementation of `DataFrame` as the base.

    This text assumes that you have worked with some kind of RDBMS in the past and draws analogies and comparison between a RDBMS table and `DataFrame` from time to time. The idea is to build upon the knowledge that you already have. However, if you have not worked with the RDBMS in the past, it's not a deal breaker. You should still be able to follow the text along.
