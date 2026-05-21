# API Documentation

Welcome to the API Documentation for the Docs platform.

## Overview

This documentation provides comprehensive information about all available APIs for managing Docs objects and their contents.

## What's Included

### Docs Creation and Management APIs

APIs for creating, retrieving, updating, and managing Docs objects:

- Create new Docs
- Retrieve Doc details by ID
- Retrieve lists of Docs by External ID
- View Doc contents and expiring contents
- Update Doc status

### Docs Update via Lists APIs

APIs for managing Docs through list operations:

- Add lists through relists or content migration
- Retrieve Doc details by Doc ID or External ID
- Cancel specific Docs

## Getting Started

To get started with the API, navigate to the relevant section in the sidebar.

All API endpoints require authentication using the `Docs-Entity-ID` header.

## Base URL

https://api.example.com

## Authentication

All requests must include:

- **Docs-Entity-ID** header: Your unique entity identifier
- **Content-Type** header: `application/json`

## Support

For questions or issues, contact our API support team.
