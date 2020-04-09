# Instruction


Origin [link](https://developers.livechat.com/docs/getting-started/guides/webhook-apps/)

1. Sign in [Developer console](https://developers.livechat.com/console/) 
2. Create new App
3. Add block "Agent App Widget", set "App Settings" field as `https://youdomain.zone/settings-page/`
	
4. Add block "App Authorization", click to "Server-side app" and click "Continue". In next page:
	* find "Redirect URI whitelist" and add `https://youdomain.zone`
	* find "Access scopes" and add `webhooks--my:rw` and `webhooks_manage`

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
	* `REDIRECT_URI_STRING ` - string from "Redirect URI whitelist" in "App Authorization" block
		
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
	* `CODE_STRING`
	* `CLIENT_ID_STRING`
	* `CLIENT_SECRET_STRING`
	* `REDIRECT_URI_STRING`