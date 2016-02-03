---
title: Mutant School API Reference

language_tabs:
  - http
  - shell: cURL
  - ruby
  - javascript: JS/jQuery

toc_footers:
  - From your friends at Mutantcorp.

includes:
  - mutants_index
  - mutants_show
  - mutants_create
  - mutants_update
  - mutants_destroy
  - terms_index
  - terms_show
  - terms_create
  - terms_update
  - terms_destroy
  - enrollments_index
  - enrollments_show
  - enrollments_create
  - enrollments_destroy
  - term_enrollments_index
  - term_enrollments_show
  - term_enrollments_create
  - term_enrollments_destroy
  - advisees_index
  - advisees_create
  - advisees_destroy


search: true
---

# Introduction

Welcome to the Mutant School API! Use our API endpoints to get (or add to) the details of the students, enrollment periods, and advisors in our fine school.

There is no authentication of any sort in this release of the API, so knock yourself out.

<aside class="warning">Are there any automated tests for this thing? It seems like there ought to be. Try to use one of those fancy <em>gem</em> whatsits you're always talking about. <em>&mdash; Boss Person</em></aside>

You'll find code examples in the dark area to the right, and you can toggle between programming languages for each example using the tabs in the top right. We have raw HTTP requests, cURL commands, Ruby, or JavaScript (jQuery, to be precise), because why the heck not?

<aside class="notice">Code examples are provided to give you an easy way to try out the endpoints. They're not necessarily meant to dictate your approach to hitting the API programmatically. If you want to HTTParty, for example (in which case you must party hard), feel free.</aside>
