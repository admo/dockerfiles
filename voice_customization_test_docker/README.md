Building
```sh
docker build . --tag ubuntu:voice_customization_test
```

Using
```sh
docker run --mount type=bind,source=path/to/sparta/sparta,target=/workspace/sparta --mount type=bind,source=path/to/voice_tools,target=/workspace/voice_tools --rm --tty --interactive ubuntu:voice_customization_test bash
```
