# Frequently Asked Questions (FAQ)

### How do I set up an alternative AI model?

The workflow offers the ability to change the API end points and override model names in the [Workflow Environment Variables](https://www.alfredapp.com/help/workflows/advanced/variables/#environment). This requires advanced configuration and is not something we can provide support for, but [our community are doing it with great success and can help you](https://www.alfredforum.com/topic/21544-using-alternative-and-local-models-with-the-chatgpt-dall-e-workflow/).

### How do I access the service behind a proxy?

Add a new https_proxy key in [Workflow Environment Variables](https://www.alfredapp.com/help/workflows/advanced/variables/#environment). Or configure the proxy for all workflows under Alfred Preferences → Advanced → Network.

### Why can’t I use the workflow with a ChatGPT Plus subscription?
[The ChatGPT API and ChatGPT Plus subscription are billed separately.](https://help.openai.com/en/articles/6950777-what-is-chatgpt-plus#h_e3d911c532)

### How can I reuse pre-made prompts?

Make a new workflow with a [Keyword Input](https://www.alfredapp.com/help/workflows/inputs/keyword/) and connect it to an [Arg and Vars Utility](https://www.alfredapp.com/help/workflows/utilities/argument/) with your custom prompt text plus `{query}`, which will be replaced with new input from the Keyword. Then connect it to a [Call External Trigger Output](https://www.alfredapp.com/help/workflows/outputs/call-external-trigger/) set to open `continue_chat` from this workflow.

### Is there a video which shows how to use the workflow?

[Yes.](https://youtube.com/watch?v=eNPMqyV8psY)

### Why does nothing happen when I run the workflow?

Something always happens, so check the [debugger](https://www.alfredapp.com/help/workflows/advanced/debugger/). Ensure you [installed the Automation Tasks](https://www.alfredapp.com/help/kb/automation-task-not-found/).

### How do I report an issue?

Accurate and thorough information is crucial for a proper diagnosis. **At a minimum, your report should include:**

* The [debugger](https://www.alfredapp.com/help/workflows/advanced/debugger/) output of the failing action.
* Your installed versions of: the Workflow, Alfred, and macOS. *Be precise, don’t say “latest”.*

### Why do I keep getting Quota exceeded?

You need API credits to use the workflow. You can [view your remaining credits and top up your account on the OpenAI website](https://platform.openai.com/account/billing/overview).

### Why do I keep getting `[Connection Stalled]`?

This happens when the workflow takes too long to receive a reply from the API. It indicates a problem either with your connection or OpenAI’s service.

[Open a terminal](https://support.apple.com/en-gb/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac) and run the following (replace `YOUR_API_KEY` within the quotes with your API key):

```console
openai_key="YOUR_API_KEY"
time /usr/bin/curl "https://api.openai.com/v1/chat/completions" --header "Authorization: Bearer ${openai_key}" --header "Content-Type: application/json" --data '{ "model": "gpt-3.5-turbo", "messages": [{ "role": "user", "content": "What is red?" }], "stream": true }'
```

It should provide a clue as to what is happening. Include the result in your report.
