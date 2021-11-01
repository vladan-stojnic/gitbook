---
description: Appropriate limits and guidelines for logging data to Weights & Biases
---

# Limits & Performance

### Best Practices for Fast Page Loading

For fast page loading in the W\&B UI, we recommend keeping logged data amounts within these bounds.

* **Scalars**:** **you can have tens of thousands of steps and hundreds of metrics
* **Histograms**: we recommend limiting to thousands of steps

If you send us more than that, your data will be saved and tracked, but pages may load more slowly.

### Python Script Performance

There are few common ways the performance of your python script can be reduced:

1. The size of your data is too large. The larger the size of the data the latency could be around 1ms in addition to the training loop.
2. The speed of your network and the how the W\&B backend is configured
3. Calling  `wandb.log` more than a few times per second. This is due to a small latency added to the training loop every time `wandb.log` is called.  &#x20;

{% hint style="info" %}
Is frequent logging slowing your training runs down? Check out [this Colab](http://wandb.me/log-hf-colab) for methods to get better performance by changing your logging strategy.
{% endhint %}

We do not assert any limits beyond rate limiting. Our Python client will automatically do an exponential backoff and retry requests that exceed limits, so this should be transparent to you. It will say “Network failure” on the command line. For unpaid accounts, we may reach out in extreme cases where usage exceeds reasonable thresholds.&#x20;

### Rate Limits

The W\&B API is rate limited by IP and API key. New accounts are restricted to 200 requests per minute. This rate allows you to run approximately 15 processes in parallel and have them report without being throttled. If the **wandb** client detects it's being limited, it will backoff and retry sending the data in the future. If you need to run more than 15 processes in parallel send an email to [contact@wandb.com](mailto:contact@wandb.com).

For sweeps, we support up to 20 parallel agents.

### Size Limits

#### Files

The maximum file size for new accounts is 2GB. A single run is allowed to store 10 GB of data. If you need to store larger files or more data per run, contact us at [contact@wandb.com](mailto:contact@wandb.com).

#### Metrics

Metrics are sampled to 1500 data points by default before displaying in the UI.&#x20;

#### Logs

While a run is in progress we tail the last 5000 lines of your log for you in the UI. After a run is completed the entire log is archived and can be downloaded from an individual run page.

**Config**

We support up to 15MB of serialized config data per run.

### Logging Guidance

Here are some additional guidelines for logging data to W\&B.

* **Nested parameters**: We automatically flatten nested parameters, so if you pass us a dictionary we will turn it into a dot-separated name. For config values, we support 3 dots in the name. For summary values, we support 4 dots.
