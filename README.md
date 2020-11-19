## GitFlow 开发流程说明

采用Github作为代码托管平台，使用GitFlow作为代码提交发布流程是非常有效的。特别是针对多人协作项目，需要Review代码的项目。同时也非常利于CI/CD的实现；

GitFlow使用时需要保持分支的整洁和采用正确的命名规则。GitFlow只有两个永久分支（develop，master），对于新的项目也可以采用main替换master分支名称。
特别说明：网上有开源的git flow工具，但个人觉得使用起来并不方便，特别是针对github作为代码托管平台，同时还需要做code review。

### 开发流程：
开发工作全部在develop分支基础上创建新的分支进行。新分支采用feature/name作为前缀表明这个是一个新功能开发。采用bugfix/name作为bug修改。然后通过发起pull request的方式合并到develop分支。可能还有其他前缀的命名，这个待发现，我现在能想到的只有feature和bugfix。
#### 提交规则：
* 对于所有的pull request必须要经过代码review才能合并，保证代码质量。
* 同时对于commit message必须做到清晰，明确，bugfix要写明发生的原因和修正的方法。
* 同时可以基于当前的pull request编号，添加CHANGELOG.md,格式参照项目上传的demo log。
* 对于pull request可以采用多次提交，每次提交只改特定的功能，这样提交日志更加清晰。
* 合并方法，参照文档[merge method](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/about-merge-methods-on-github),有三种merge方法，在项目的Settings->Options中可以选择支持的merge方法，个人建议采用squash merge的方法，这个方法会将分支上的提交合并为一个新的commit，因为这些分支本身是会立即删除的，这样的话提交的commit会比较美观；

### 发布预热：
当需要发布新的版本时，需要从develop分支上创建新的release分支，release分支命名为release/vx.x.x。建议采用major，minor，patch三位作为版本号。在定义relase分支时最好和产品开会，确保完成了所有feature的开发，同时必须要保证不能在加入新的feature。relase分支只支持测试发现的bug修正，即只能pull request bugfix/xxx分支。当release分支完成开发并通过测试后，进入实际的发布流程。


### 版本发布：
将release/vx.x.x合并到develop分支和master分支。然后在master分支上打tag，tag采用vx.x.x作为名称，需要保证和release分支版本号保持一致。同时如果集成了CI/CD流程可以通过github workflow直接触发发布流程，打包上传到相关平台进行发布操作。

### 特别说明：
* 1、github由于经常被墙，所以采用github需要自备梯子；
* 2、github对于个人开发者是免费的，但对于企业用户是需要按人头收费的，同时对于后期做CI/CD的github workflow也是需要收费的。但相对于自己租服务器还是实惠很多的；

