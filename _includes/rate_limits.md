
<!---DEFAULT RATE LIMIT-->

{% if include.endpoint == "default" %}
We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---PUT /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "update dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "look up dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---DELETE /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "delete dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---POST /scim/v2/Users--->
{% elsif include.endpoint == "create dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and DELETE endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users--->
{% elsif include.endpoint == "look up dashboard user email" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).


<!---/users/external_id/rename-->
<!---/users/external_id/remove-->

{% elsif include.endpoint == "external id migration" %}
We apply a rate limit of 1,000 requests per minute to this endpoint, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/track-->

{% elsif include.endpoint == "users track" %}
We apply a base speed limit of 50,000 requests per minute to this endpoint for all customers. Each `/users/track` request can contain up to 75 event objects, 75 attribute objects, and 75 purchase objects. Each object (event, attribute, and purchase arrays) can update one user each. In total, this means a max of 225 users can be updated in a single call. In addition, a single user profile can be updated by multiple objects.

See our page on [API rate limits]({{site.baseurl}}/api/api_limits/) for details, and reach out to your customer success manager if you need your limit increased.

<!---/users/export/ids-->

{% elsif include.endpoint == "users export ids" %}
For customers who onboarded with Braze on or after August 16, 2021, we apply a rate limit of 2,500 requests per minute to this endpoint, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/delete-->

{% elsif include.endpoint == "users delete" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/alias/new`, `/users/identify`, and `/users/merge` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/alias/new-->

{% elsif include.endpoint == "users alias new" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/identify`, `/users/merge`, and `/users/alias/update` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/identify`, `/users/merge`, and `/users/alias/new` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/identify`, and `/users/merge` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/identify-->

{% elsif include.endpoint == "users identify" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/alias/new`, `/users/merge`, and `/users/alias/update` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/merge-->

{% elsif include.endpoint == "users merge" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/alias/new`, `/users/identify`, and `/users/alias/update` endpoints, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/events/list-->

{% elsif include.endpoint == "events list" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 1,000 requests per hour to this endpoint. This rate limit is shared with the `/purchases/product_list` endpoint, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/purchases/product_list-->

{% elsif include.endpoint == "purchases product list" %}
For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 1,000 requests per hour to this endpoint. This rate limit is shared with the `/events/list` endpoint, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/messages/send-->
<!---/campaigns/trigger/send-->
<!---/canvas/trigger/send-->

{% elsif include.endpoint == "send endpoints" %}
When specifying a segment or Connected Audience in your request, we apply a rate limit of 250 requests per minute to this endpoint. Otherwise, if specifying an `external_id`, this endpoint has a default rate limit of 250,000 requests per hour, as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/transactional/v1/campaigns/YOUR_CAMPAIGN_ID_HERE/send -->

{% elsif include.endpoint == "transactional email" %}
Transactional Emails are not subject to a rate limit. Depending on your chosen package, a set number of Transactional Emails is covered per hour by SLA. Requests that exceed that rate will still send, but are not covered by SLA. 99.9% of emails will send in less than one minute.

<!---/sends/id/create-->

{% elsif include.endpoint == "sends id create" %}
The daily maximum number of custom send identifiers that can be created via this endpoint is 100 for a given app group. Each `send_id` and `campaign_id` combination that you create will count towards your daily limit. The response headers for any valid request include the current rate limit status, see [API rate limits]({{site.baseurl}}/api/api_limits/) for details.

<!---/subscription/status/set-->
{% elsif include.endpoint == "subscription status set" %}
For customers who onboarded with Braze on or after January 6, 2022, we apply a rate limit of 5,000 requests per minute shared across the `/subscription/status/set` and `/v2/subscription/status/set` endpoint as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

{% endif %}

<!---Additional if statement for Messaging endpoints-->

{% if include.category == "message endpoints" %}

Braze endpoints support [batching API requests]({{site.baseurl}}/api/api_limits/#batching-api-requests). A single request to the messaging endpoints can reach any of the following:

- Up to 50 specific `external_ids`, each with individual message parameters
- A segment of any size created in the Braze dashboard, specified by its `segment_id`
- An ad-hoc audience segment of any size, defined in the request as a [Connected Audience]({{site.baseurl}}/api/objects_filters/connected_audience/) object

{% endif %}
