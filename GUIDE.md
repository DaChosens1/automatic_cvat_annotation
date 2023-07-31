## Guide to setting up Automatic Annotation
Connected Repo: [https://github.com/DaChosens1/automatic_cvat_annotation.git](https://github.com/DaChosens1/automatic_cvat_annotation.git)

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

Then, in the path `/cvat/serverless`, git clone [this repo](https://github.com/DaChosens1/automatic_cvat_annotation.git)
```
git clone https://github.com/DaChosens1/automatic_cvat_annotation.git
```

Edit `custom-yolov8-origin` folder files, `function.yaml` and the model pathway in `main.py` based on the comments. Refer to `custom-yolov8` folder as an example using the chevron model named `chevron.pt`.

To deploy a function for cvat to use, we can use the serverless/deploy_cpu.sh for linux, but for all users we will use nuctl dirctly. You can view your deployed functions by running `nuctl get functions` or going to the website `localhost:8070`, the hosted nuclio homepage
```
nuctl create project cvat
nuctl deploy --project-name cvat --path "./serverless/<custom_directory_name>/<desired_subdir_model_setup>" --platform local
```

The model setup should be good to go! 
- Inside of cvat, on the 3 dots on the right of a task, there should be an option for `automatic annotation` to use a detector model on all frames
- the models page should list hosted models
- inside of a job, under AI Tools -> Detector should list detection type models; -> Tracker should list tracker type models. Running detection should run the model on 1 frame, while tracker will run the model when you switch to the next frame.

If you have issues, contact Gregory Li, look at [Common Issues](https://github.com/DaChosens1/automatic_cvat_annotation/blob/DaChosens1-patch-1/COMMON_ISSUES.md), or look at resources.

## Resources
- https://opencv.github.io/cvat/docs/manual/advanced/serverless-tutorial/
- https://opencv.github.io/cvat/docs/administration/advanced/installation_automatic_annotation/
- https://opencv.github.io/cvat/docs/manual/advanced/ai-tools/
- https://opencv.github.io/cvat/docs/manual/advanced/automatic-annotation/
- https://github.com/kurkurzz/custom-yolov8-auto-annotation-cvat-blueprint
