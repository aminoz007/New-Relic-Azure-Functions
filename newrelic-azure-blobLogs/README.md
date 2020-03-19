# NewRelic-Azure Blobs logs forwarder

This function is used to forward Azure logs from new blob files added in a storage account to New Relic logs collector. This function sends each line in a blob file as log entry to New Relic.

This project is provided AS-IS WITHOUT WARRANTY OR SUPPORT, although you can report issues and contribute to the project here on GitHub.

## Configuration

These parameters are provided with this function and can be configured via the [Azure function apps settings](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings).

The provided Node.js script must be deployed into your Azure Functions service.

| Property | Required or Optional | Default Value | Description
|---|---|---|---|
| NR_LICENSE_KEY | Required if `NR_INSERT_KEY` is not provided | | Your New Relic License key |
| NR_INSERT_KEY | Required if `NR_LICENSE_KEY` is not provided | | Your New Relic Insights Insert key |
| NR_ENDPOINT|  Optional | `https://log-api.newrelic.com/log/v1` | New Relic ingestion endpoint |
| NR_TAGS | Optional | | Key value pairs seperated by semicolon  to tag all logs sent to New Relic (example: `env:prod;team:myTeam`) |
| NR_MAX_RETRIES | Optional | 3 | Determines how many times we should retry sending the logs in case of network failures |
| NR_RETRY_INTERVAL | Optional | 2000 (= 2 seconds) | Determines how long we should wait before we retry sending the logs in case of network failures (in milliseconds) |

## Deployment

1. Log in to the Azure Portal.
2. Cick on the top left `+` icon then Compute then Function App.
3. Once you click on Function App, the next screen will appear where you need to provide some information. Select:
* Publish: code 
* Runtime stack: Node.js 
* Version: 12 
* Operating System: Windows  
Fill out the other information (region, subscription, hosting etc ...)
4. After this function is deployed we will need to add a trigger. Click on the `+` icon next to Functions and then click on In-Portal to code in the Azure portal itself.
5. Now we must select the desired template from the available templates. Click on `more templates` and select `Azure Blob Storage trigger`.
6. Add the wanted `Storage account connection` or create a new one if you haven't have one already. Select the `Path` and the `Function Name`.
7. Copy paste the code of the [New Relic - Azure function](./index.js). Make sure that under `Integrate` section:
a. `Blob Parameter Name` is set to `myBlob`.

### EU image configuration

If you are running this function in the EU set the `NR_ENDPOINT` to `https://log-api.eu.newrelic.com/log/v1`.

### Getting Your Keys

* Getting your New Relic Insights Insert key:
`https://insights.newrelic.com/accounts/<ACCOUNT_ID>/manage/api_keys`

* Getting your New Relic license key:
`https://rpm.newrelic.com/accounts/<ACCOUNT_ID>`

## Issues / Enhancement Requests

Issues and enhancement requests can be submitted in the [issues tab of this repository](https://github.com/aminoz007/New-Relic-Azure-Functions/issues).
Please search for and review the existing open issues before submitting a new issue.

## Contributing

Contributions are welcome (and if you submit a Enhancement Request, expect to be invited to contribute it yourself :grin:).
