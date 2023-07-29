## Guide to setting up Automatic Annotation
Make sure you are at root directory, where you have already cloned `cvat`! This should work for both Mac and Linux. If you have Windows, you may need to do a bit of digging in the official docs and forums D:

- First you need to start up `cvat` in docker in serverless mode

Typically:
```
docker-compose up -d
docker-compose down
```
Instead:
```
docker compose -f docker-compose.yml -f components/serverless/docker-compose.serverless.yml up -d
docker compose -f docker-compose.yml -f components/serverless/docker-compose.serverless.yml down
```
- Next, you have to install `nuctl` command line tool to build and deploy serverless functions, which will make the model avaliable for `cvat`. Download version [1.8.14](https://github.com/nuclio/nuclio/releases/tag/1.8.14). It is important that the version you download matches the version in docker-compose.serverless.yml, and other specs matches your system. For example, using wget.

System fill in
- Mac: `darwin`
- Linux: `linux`
```
wget https://github.com/nuclio/nuclio/releases/download/1.8.14/nuctl-1.8.14-<system>-amd64
```
Then give it the proper permissions and do a softlink.
```
sudo chmod +x nuctl-1.8.14-<system>-amd64
sudo ln -sf $(pwd)/nuctl-1.8.14-<system>-amd64 /usr/local/bin/nuctl
```


## Resources
- https://opencv.github.io/`cvat`/docs/manual/advanced/serverless-tutorial/
- https://opencv.github.io/`cvat`/docs/administration/advanced/installation_automatic_annotation/
