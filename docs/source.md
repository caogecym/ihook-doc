---
id: source
title: Source
---

When configuring notification conditions, you may use the following source for evaluation.

| Source Type | Description |
| :------- | :----- |
| Response Code | Condition evaluation is performed on the value of the HTTP status code from the response. |
| Response Body (JSON) | Parse the response body as JSON. You must include a Property with the [JsonPath](/docs/doc-property) to assert on. |
| Response Body (Text) | Parse the response body as plain text (string). This source does not specify a Property. |