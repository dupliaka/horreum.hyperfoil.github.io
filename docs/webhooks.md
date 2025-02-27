# Webhooks

In the [regression testing guide](/docs/regression.html) you've seen how can you inform users about changes in your project's performance. You can use another mechanism to notify other services about noteworthy events, e.g. bots commenting on version control system, updating status page or triggering another job in CI: the webhooks.

Since calling arbitrary services in the intranet is security-sensitive Horreum admin has to set up a list of allowed URL prefixes (e.g. domains). As a user with the `admin` role you can see 'Global WebHooks' link in the navigation bar on the top; go there and hit the 'Add prefix' button:

<div class="screenshot"><img src="/assets/images/webhooks/00_prefix.png"></div>

When you save the modal you will see the prefix appearing in the table. Then in the lower half of the screen you can add global webhooks: whenever a new Test is created, a Run is uploaded or Change is emitted Horreum can issue a HTTP POST request to this URL, using the new JSON-encoded entity as a request body. You can also use a JSON path[^1] wrapped in `${...}`, e.g. `${$.data.foo}` in the URL to refer to the object sent.

<div class="screenshot"><img src="/assets/images/webhooks/01_globalhook.png"></div>

Test owners can set webhooks for individual tests, too. Go to the Test configuration, 'Webhooks' tab and press the 'New Webhook' button. This works identically to the global webhooks.

<div class="screenshot"><img src="/assets/images/webhooks/02_testhook.png"></div>

Even though non-admins (in case of global hooks) and non-owners of given test cannot see the URL is is adviseable to not use any security sensitive tokens.

[^1]: In this case the JSON path is evaluated in the application, not in PostgreSQL, therefore you need to use the [Jayway JSON Path syntax](https://github.com/json-path/JsonPath) - this is a port of the original Javascript JSON Path implementation.