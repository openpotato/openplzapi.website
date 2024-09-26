# Paging

Most API endpoints in the OpenPLZ API project implement the so-called **Paging**.

## What is paging?

Paging in web services is a technique to divide the results of large amounts of data into smaller, manageable parts. Instead of sending all the results of a query at once, the content is divided into pages so that a client can access different pages sequentially or on demand.

## Why paging?

Let's start with an example. The following request:

```
GET https://openplzapi.org/de/Streets?locality=Berlin
```

would return 15335 streets without paging. This is quite a lot and would place a disproportionate load on the server, increase network latency and lengthen response times. It is better to transfer this data in instalments, in so-called pages. You can configure the size of the the page, when you call it up. 

## How exactly does paging work?

Paging is configured using special URL parameters in the API call. This specifies which page of results the client wants to see and how many results should be displayed per page. The URL parameters are called:

1. `page`: The index of the page that is requested.
2. `pageSize`: The number of elements per page.

This request returns the first 10 addresses for Berlin:

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=1&pageSize=10
```

The next request returns the following 10 addresses for Berlin:

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=2&pageSize=10
```

If the URL parameter `page` is omitted from the request, the default value `page=1` applies. If the URL parameter `pageSize` is omitted from the request, the default value `pageSize=50` applies. The request

```
GET https://openplzapi.org/de/Streets?locality=Berlin
```

therefore corresponds to the request

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=1&pageSize=50
```

The maximum size for a page is 50.

## How do I know how many pages there are?

If an API request responds successfully, additional information is supplied in the [HTTP response headers](https://developer.mozilla.org/docs/Web/HTTP/Headers). Let's take a look at a typical response header list:

```
content-security-policy: default-src https: data: ‘unsafe-inline’ 
content-type: text/json; charset=utf-8 
date: Thu,26 Sep 2024 09:26:48 GMT 
permissions-policy: accelerometer=(),camera=(),geolocation=(),gyroscope=(),magnetometer=(),microphone=(),payment=(),usb=(),interest-cohort=() 
referrer-policy: strict-origin-when-cross-origin 
server: nginx 
strict-transport-security: max-age=2592000 
x-content-type-options: nosniff 
x-frame-options: SAMEORIGIN  
x-page: 1 
x-page-size: 10 
x-total-count: 15335 
x-total-pages: 1534 
```

The last four values are of interest to us here:

1. `x-page`: The index of the page that was requested.
2. `x-page-size`: The number of elements per page.
3. `x-total-count`: The total number of elements for this request.
4. `x-total-pages`: The number of pages for this request.

These values are returned for all API endpoints that implement paging.

!!! note "Why not in the JSON payload?"

    The OpenPLZ API returns the paging metadata in the HTTP response headers. There are other implementations that return this information as part of the JSON payload that represents the actual response. We have decided against this because we support not only JSON but also CSV as a payload format.

## API endpoints without paging

Some API endpoints do not implement paging, as the resulting data volume is manageable:

+ `at/FederalProvinces`
+ `ch/Cantons`
+ `de/FederalStates`
+ `li/Communes`

