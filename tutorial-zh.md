# 初创团队 IT 治理样板间

## 简介

当您注册了一个新的阿里云账号之后，我们建议您不要立刻开始使用云上资源构建业务系统，相反，需要先花一点时间来进行一些初步设置。这是为了保障您账号最基本的安全性、运维便捷性而进行的最小化配置。

本教程介绍了使用 Terraform 自动的完成相关账号初始化的工作。

<tutorial-nav></tutorial-nav> 

## RAM 配置

您可以通过 Terraform 完成基本的用户组配置，方便后续RAM用户的简单授权。Cloud Shell 中内置了 Terraform 和您的身份信息，您可以直接使用。

首先，您需要定位到用来配置 RAM 的 Terraform 模板的目录。

```bash
cd ~/tutorial-landing-zone-one-terraform/ram
```

然后执行 `init`，保证加载 [alicloud providers](https://www.terraform.io/docs/providers/alicloud/index.html)

```bash
terraform init
```

最后，您就可以一键完成基本的 RAM 配置。

```bash
terraform apply
```

其中，您可以打开 <tutorial-editor-open-file filePath="tutorial-landing-zone-one-terraform/ram/main.tf">ram/main.tf 文件</tutorial-editor-open-file>查看完整的 Terraform 模板。该模板为您配置了：

- 设置了 RAM 用户密码强度
- 创建了 CloudAdminGroup 用户组，同时为该组授予了 AdministratorAccess 权限，加入该组的用户可以获得对云上资源的完全访问权限。
- 创建了 SystemAdminGroup 用户组，为该组授予了自定义权限。如果您的团队有更详细分工，可以进一步创建诸如数据库管理员（DBA）、网络管理员等用户组并授予合适产品的权限，再将人员加入相应的组。
- 创建了 BillingAdminGroup 用户组，同时授予 AliyunBSSFullAccess 和 AliyunFinanceConsoleFullAccess 权限，您的财务人员可以加入该组，获取云上财务、账单的相应权限。
- 创建了 CommonUserGroup 用户组，用户组织普通用户。如果您的企业有统一的权限要求，例如只允许从公司内网访问阿里云，您需要编写合适的自定义策略，并授权给CommonUserGroup组。

您现在可以登录 [RAM 访问控制控制台](https://ram.console.aliyun.com/overview)查看通过 Terraform 完成的 RAM 配置。

## 网络配置

您可以继续通过 Terraform 完成基本的网络配置，包括创建专有网络、安全组等。

首先，您需要定位到用来配置网络的 Terraform 模板的目录。

```bash
cd ~/tutorial-landing-zone-one-terraform/vpc
```

然后执行 `init`，保证加载 [alicloud providers](https://www.terraform.io/docs/providers/alicloud/index.html)

```bash
terraform init
```

最后，您就可以一键完成基本的网络配置。

```bash
terraform apply
```

其中，您可以打开 <tutorial-editor-open-file filePath="tutorial-landing-zone-one-terraform/vpc/main.tf">vpc/main.tf 文件</tutorial-editor-open-file>查看完整的 Terraform 模板。该模板为您配置了：

- 创建了名为 `default_vpc` 的专有网络
- 在上述 vpc 下创建了名为 `default_vswitch` 的交换机
- 创建默认安全组

您现在可以登录[专有网络（VPC）控制台](https://vpcnext.console.aliyun.com/)查看通过 Terraform 完成的网络配置。

## 云账号安全加固（推荐）

建议您对自己的云账号进行安全设置，包括修改登录密码和开启多因素认证（Multi-factor authentication，MFA）。同时创建并授权用于管理操作的RAM用户，从而最大化减少云账号的使用。

该操作需要在控制台中进行，详细步骤，您可以参考：

- [云账号安全设置](https://help.aliyun.com/document_detail/170395.html)
- [创建 admin 用户并加固安全设置](https://help.aliyun.com/document_detail/170396.html)

## 总结

至此您已经成功使用 Terraform 完成最基本的阿里云账号初始化操作及基础环境搭建流程，其不包含任何业务系统，目的是通过定义基本的用户访问框架，并配合一些后续使用原则来保证账号的基础安全性。这个简单框架并不能涵盖一个典型企业的完整IT治理需求，因此您可以在此基础上根据自己企业的实际情况进行补充和裁剪。

如需了解更多内容，请访问[企业 IT 治理](https://help.aliyun.com/document_detail/172542.html)