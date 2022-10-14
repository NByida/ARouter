### arouter插件编译失败，编译环境：
  - gradle ：7.2.0
  - agp:7.0.0

### 在使用 @Autowired 注解后编译，报错如下：
```
then the AS will threw an exception:
NextHost requires ASM7.
```

### 解决方案


####  自行修改Arouter代码，生成新的插件替换

- fork arouter代码
- 全局替换Opcodes.ASM5 为 Opcodes.ASM7
- 执行 publish.uploadArchives() 在build/localMaven下会生成二进制Plugin插件
- 添加本地maven仓库地址
```
   maven {
            url = "${rootProject.getPath()}/../localMaven"
        }

    dependencies {
        ...
        classpath 'com.alibaba:arouter-register-asm7:1.0.2'
        ...
        }
```

### 这里已经把新版插件编译完成了，直接使用就好

使用步骤：

- 1 复制/localMaven目录下面的文件到 根目录下面
- 2 在项目的build.gradle添加本地仓库地址

```
   maven {
            url = "${rootProject.getPath()}/../localMaven"
        }

    dependencies {
        ...
        //删除原先的classpath "com.alibaba:arouter-register:$arouter_register_version"
        //使用我们刚刚/localMaven下的新jar包
        classpath 'com.alibaba:arouter-register-asm7:1.0.2'
        ...
        }
```






