# lambda-response-template

[![npm version](https://badge.fury.io/js/lambda-response-template.svg)](https://badge.fury.io/js/lambda-response-template)
[![Build Status](https://travis-ci.com/c-bandy/lambda-response-template.svg?branch=master)](https://travis-ci.com/c-bandy/lambda-response-template)
[![codecov](https://codecov.io/gh/c-bandy/lambda-response-template/branch/master/graph/badge.svg)](https://codecov.io/gh/c-bandy/lambda-response-template)
[![dependencies Status](https://david-dm.org/c-bandy/lambda-response-template/status.svg)](https://david-dm.org/c-bandy/lambda-response-template)

>💬 A tiny utility for creating AWS Lambda response objects.

This package provides an easy free way for you generate templates for your responses. Helps reduce clutter and make your
output more consistent across your Lambda application.

## Install

```bash
npm install lambda-response-template
```

## Features

* Templating
  * Create templates for your responses.
* Normalizes headers
  * Always outputs headers with the same case.

## Why

When developing large applications you often work across multiple repositories. I found myself following the same
pattern of creating a factory in each repository every time I wanted set standards for a lambda's output. When you also
have to add tests for this boilerplate it can quickly get annoying - this package aims to solve this problem by creating
a first class, best version of this generic method, that is easily accessible as a module.

## Usage

Set up lambda-response-template your defaults:

```typescript
import { ResponseTemplate } from 'lambda-response-template';

const reply = new ResponseTemplate({
  headers: {
    'x-powered-by': 'nodejs',
  }
});
```

And then use inside your function:

```typescript
async function handler(event, context) {
  return reply.make(200, '{"message": "Hello world!"}', options);
}
```

Your response will be made from the template, inheriting any options you set.

## Tips

```typescript
// a === b

const a = reply.make(200, 'Hello world', { headers: { 'Content-Type': 'text/plain' }});

const b = reply.make(200, 'Hello world', 'text/plain');
```