load("//build:workspace_mirror.bzl", "mirror")
load("//build:workspace.bzl", "CRI_TOOLS_VERSION")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "242602c9818a83cbe97d1446b48263dcd48949a74d713c172d1b03da841b168a",
    urls = mirror("https://github.com/bazelbuild/rules_go/releases/download/0.10.5/rules_go-0.10.5.tar.gz"),
)

http_archive(
    name = "io_kubernetes_build",
    sha256 = "007774f06536059f3f782d1a092bddc625d88c17f20bbe731cea844a52485b11",
    strip_prefix = "repo-infra-97099dccc8807e9159dc28f374a8f0602cab07e1",
    urls = mirror("https://github.com/kubernetes/repo-infra/archive/97099dccc8807e9159dc28f374a8f0602cab07e1.tar.gz"),
)

http_archive(
    name = "bazel_skylib",
    sha256 = "bbccf674aa441c266df9894182d80de104cabd19be98be002f6d478aaa31574d",
    strip_prefix = "bazel-skylib-2169ae1c374aab4a09aa90e65efe1a3aad4e279b",
    urls = mirror("https://github.com/bazelbuild/bazel-skylib/archive/2169ae1c374aab4a09aa90e65efe1a3aad4e279b.tar.gz"),
)

ETCD_VERSION = "3.2.18"

new_http_archive(
    name = "com_coreos_etcd",
    build_file = "third_party/etcd.BUILD",
    sha256 = "b729db0732448064271ea6fdcb901773c4fe917763ca07776f22d0e5e0bd4097",
    strip_prefix = "etcd-v%s-linux-amd64" % ETCD_VERSION,
    urls = mirror("https://github.com/coreos/etcd/releases/download/v%s/etcd-v%s-linux-amd64.tar.gz" % (ETCD_VERSION, ETCD_VERSION)),
)

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "c440717ee9b1b2f4a1e9bf5622539feb5aef9db83fc1fa1517818f13c041b0be",
    strip_prefix = "rules_docker-8bbe2a8abd382641e65ff7127a3700a8530f02ce",
    urls = mirror("https://github.com/bazelbuild/rules_docker/archive/8bbe2a8abd382641e65ff7127a3700a8530f02ce.tar.gz"),
)

load("@bazel_skylib//:lib.bzl", "versions")

versions.check(minimum_bazel_version = "0.13.0")

load("@io_bazel_rules_go//go:def.bzl", "go_download_sdk", "go_register_toolchains", "go_rules_dependencies")
load("@io_bazel_rules_docker//docker:docker.bzl", "docker_pull", "docker_repositories")

go_rules_dependencies()

go_register_toolchains(
    go_version = "1.10.3",
)

docker_repositories()

http_file(
    name = "kubernetes_cni",
    sha256 = "f04339a21b8edf76d415e7f17b620e63b8f37a76b2f706671587ab6464411f2d",
    urls = mirror("https://storage.googleapis.com/kubernetes-release/network-plugins/cni-plugins-amd64-v0.6.0.tgz"),
)

http_file(
    name = "cri_tools",
    sha256 = "ccf83574556793ceb01717dc91c66b70f183c60c2bbec70283939aae8fdef768",
    urls = mirror("https://github.com/kubernetes-incubator/cri-tools/releases/download/v%s/crictl-v%s-linux-amd64.tar.gz" % (CRI_TOOLS_VERSION, CRI_TOOLS_VERSION)),
)

docker_pull(
    name = "debian-iptables-amd64",
    digest = "sha256:0987db7ce42949d20ed2647a65d4bee0b616b4d40c7ea54769cc24b7ad003677",
    registry = "k8s.gcr.io",
    repository = "debian-iptables-amd64",
    tag = "v10.2",  # ignored, but kept here for documentation
)

docker_pull(
    name = "debian-hyperkube-base-amd64",
    digest = "sha256:c50522965140c9f206900bf47d547d601c04943e1e59801ba5f70235773cfbb6",
    registry = "k8s.gcr.io",
    repository = "debian-hyperkube-base-amd64",
    tag = "0.10.2",  # ignored, but kept here for documentation
)

docker_pull(
    name = "official_busybox",
    digest = "sha256:4cee1979ba0bf7db9fc5d28fb7b798ca69ae95a47c5fecf46327720df4ff352d",
    registry = "index.docker.io",
    repository = "library/busybox",
    tag = "latest",  # ignored, but kept here for documentation
)

load("//build:workspace_mirror.bzl", "export_urls")

export_urls("workspace_urls")
