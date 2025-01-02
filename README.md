# Example app: Joke

This app makes jokes based on the provided context.

## Usage

You need a Unix-compatible (macOS, Linux or Windows [WSL](https://learn.microsoft.com/en-us/windows/wsl/install))
system to run this app. Open a terminal and execute the steps below:

You need to specify the OpenAI API key as shown below.

```shell
export OPENAI_API_KEY="FIXME"
```

You may run this app without making a local copy first (i.e. clone the repo)
using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent clonerun https://github.com/agentlang-hub/joke.git
```

### Running a local copy of the app

If you have cloned the app and made a local copy on your computer,
you may run it using Docker as follows:

```shell
docker run --rm \
  -p "0.0.0.0:8080:8080" \
  -v $PWD:/agentlang \
  -e OPENAI_API_KEY="$OPENAI_API_KEY" \
  -it agentlang/agentlang.cli:latest \
  agent run
```

Alternatively, instead of Docker you may use the locally installed
[Agentlang CLI](https://github.com/agentlang-ai/agentlang.cli):

```shell
agent run
```

### Getting the app to make a joke

In another terminal, make an HTTP request as follows:

```shell
curl -X POST localhost:8080/api/Joke.Core/TellAJoke \
  -H 'Content-type: application/json' \
  -d '{"Joke.Core/TellAJoke": {"UserInstruction": "Tell me a joke about smart scientists"}}'
```

Sample result:

```json
[{"status":"ok","result":"Why did the smart scientists break up?\n\nBecause they had too many unsolved problems in their relationship!","message":null}]
```

If you want to start a new chat-session, add a session-identifier (note the `"ChatId"` attribute) to the request:

```shell
curl -X POST localhost:8080/api/Joke.Core/TellAJoke \
  -H 'Content-type: application/json' \
  -d '{"Joke.Core/TellAJoke": {"UserInstruction": "Tell me a joke about smart scientists", "ChatId": "my-new-chat-session"}}'
```


## License

Copyright 2024-2025 Fractl Inc.

Licensed under the Apache License, Version 2.0:
http://www.apache.org/licenses/LICENSE-2.0

