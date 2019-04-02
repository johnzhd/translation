# source

[http://gopherdata.io/post/distributed_trump_finder/](http://gopherdata.io/post/distributed_trump_finder/)

# Author

Daniel Whitenack, @dwhitena on Twitter and Gophers Slack

# 构建一个分布式Trump发现者

如果你还没有听说，机器学习区有个新小子叫 [MachingBox](https://machinebox.io/)。
它很酷，且你应该了解一下。
MachingBox提供预构建Docker镜像易用，易生产，且可编排机器学习选项。
例如，你可以从MachineBox获得一个“facebox”Docker镜像用来人脸识别。
当你运行facebox，你将获得全JSON API，让你轻松教会facebox确认人脸，从图像中识别出脸，后保存训练的人脸识别模型状态。

试用了facebox让我思考关于如何将它整合进我的工作流。
特别地，我想要看怎么将MachineBox镜像作为分布式数据处理通道中的一部分，用[Pachyderm](http://pachyderm.io/)构建起来。
Pachyderm 基于Docker镜像构建、运行和管理通道，比如机器学习工作流。
因此，一体化的MachineBox镜像看上去会更自然。

于是那就是第一个（我所知的）分布式，docker化，‘Trump发现’数据通道完成的样子。
在这章节中我们将详细介绍人脸识别通道的创建过程，这是可以发现、标注图像中Donald Trump的脸的位置。
实际中，这个管道可以用来识别任意人脸，且我们将举例说明这个扩展性通过学习第二张人脸，Hillary clinton。

接下来的章节假设你有一个Pachyderm集群在运行，且`pachctl`（Pachyderm CLI 工具）连接着这个集群，且你已经注册了MachineBox（可以免费）。全部代码和更多细节介绍在[这里](https://github.com/dwhitena/pach-machine-box)。

