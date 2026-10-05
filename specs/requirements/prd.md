# Greeter Service — PRD

## Problem Statement

Teams bootstrapping new services on this platform need a minimal, known-good
reference they can point at when wiring up a fresh Go HTTP service — something
small enough to stand up in minutes but that still exercises the platform's
conventions end to end (request handling, JSON responses, error shapes). Today
there is no tiny canonical example to copy from, so each new service reinvents
these basics from scratch.

## Solution

Greeter is a small Go HTTP service with a single endpoint: given a name, it
returns a JSON greeting. It exists to be a clean, conventions-correct reference
implementation — built the way `app-factory-kaj/e2e-reference` builds its
services — that other work can be checked against or copied from.

## Actors

- **API Consumer** — any caller (a person testing the service, or another
system) that sends an HTTP request to the greeter endpoint and reads back
the JSON greeting. There is no sign-in and no per-caller distinction.

## User Stories

1. As an API Consumer, I want to call `GET /hello?name=X` and receive a JSON
 greeting that includes the name I supplied, so that I get a personalized
 response.
2. As an API Consumer, I want a clear error response when I omit the `name`
 parameter or supply an invalid one, so that I understand how to call the
 service correctly.

## Product Decisions

- **Authentication:** none — the endpoint is public with no sign-in and no
per-caller identity. *assumed*
- **Response shape:** a JSON body of the form `{"message": "Hello, <name>!"}`
on success. *assumed*
- **Missing/empty `name`:** the service responds with a `400` JSON error body
(for example `{"error": "name is required"}`) rather than a default
greeting. *assumed*

