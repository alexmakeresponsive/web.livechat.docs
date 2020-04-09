# Instruction

Origin [link](https://developers.livechat.com/docs/getting-started/guides/webhook-apps/)

## Create app

1. Sign in [Developer console](https://developers.livechat.com/console/) 
2. Create new App
3. Add block "Agent App Widget", set "App Settings" field as `https://youdomain.zone/settings-page/`
	
4. Add block "App Authorization", click to "Server-side app" and click "Continue". In next page:
	* find "Redirect URI whitelist" and add `https://youdomain.zone`
	* find "Access scopes" and add `webhooks--my:rw` and `webhooks_manage`


## Get access token

Open [Authorizing API calls
](https://developers.livechat.com/docs/getting-started/authorization/#agent-authorization-flows) page and go to [Public server-side apps](https://developers.livechat.com/docs/getting-started/authorization/#public-server-side-apps) section

1. Check "Redirect URI whitelist"
2. Open web browser and run URL
	```
	https://accounts.livechatinc.com/
		?response_type=code
		&client_id=CLIENT_ID_STRING
		&redirect_uri=REDIRECT_URI_STRING
		&state=f3NtEuZ5AuxsmnVAzcyLGm17aAaltJTv
	```
	where
	* `CLIENT_ID_STRING` - string from "Client Id" in "App Authorization" block
	* `REDIRECT_URI_STRING` - string from "Redirect URI whitelist" in "App Authorization" block
		
3. After redicect, to `redirect_uri` copy `code` from URL to `CODE_STRING`
4. Open terminal and exec:
	```
	curl --compressed "https://accounts.livechatinc.com/token" \
		-X POST \
		-d "grant_type=authorization_code&\
			code=CODE_STRING&\
			client_id=CLIENT_ID_STRING&\
			client_secret=CLIENT_SECRET_STRING&\
			redirect_uri=REDIRECT_URI_STRING"
	``` 
	where 
	* `CODE_STRING` - code from "Step 3"
	* `CLIENT_ID_STRING` - string from "Client Id" in "App Authorization" block
	* `CLIENT_SECRET_STRING` - string from "Client Secret" in "App Authorization" block
	* `REDIRECT_URI_STRING` - string from "Redirect URI whitelist" in "App Authorization" block

	terminal return json object with `access_token` - copy it in `TOKEN_ACCESS`
	

## Registration hook
	
Open [Configuration API](https://developers.livechat.com/docs/management/configuration-api) page and go to section [Register Webhook](https://developers.livechat.com/docs/management/configuration-api/#register-webhook)

1. Open terminal and exec:

	```
	curl -X POST \
		https://api.livechatinc.com/v3.1/configuration/action/register_webhook \
		-H 'Content-Type: application/json' \
		-H 'Authorization: Bearer TOKEN_ACCESS' \
		-d '{
        "url": "API_URI_STRING",
        "description": "Describtion for hook",
        "action": "ACTION_STRING",
        "secret_key": "CLIENT_SECRET_STRING"  
		}'

	```
	where
	* `TOKEN_ACCESS` - token from "Get access token" section this instruction, see "Step 4"
	* `API_URI_STRING` - you api endpoint
	* `ACTION_STRING` - action from [Actions](https://developers.livechat.com/docs/management/configuration-api/#triggering-actions), for example try `incoming_event`
	* `CLIENT_SECRET_STRING` - string from "Client Secret" in "App Authorization" block

	
## Install app

Open [User console](https://my.livechatinc.com/home) and install "App" from [Marketplace](https://my.livechatinc.com/marketplace)

For self account go to "Private Apps" and install "App"

## Insert script

Open [Setings](https://my.livechatinc.com/settings/code), find "Install LiveChat code manually", copy `script` and past it on page
where you want see "LiveChat"


## Check API

Run you API server and write something in "LiveChat"