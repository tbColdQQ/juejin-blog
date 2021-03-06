## git tag 相关命令

#### 1、查看标签,可加上参数 `-l` (列表形式列出） `-n` (附加说明)

```
git tag [-l -n]
```

#### 2、查看符合检索条件的标签 

```
git tag -l 1.*.* 
```

#### 3、查看对应标签状态 

```
git checkout 1.0.0 
```

#### 4、创建标签(本地)

```
git tag 1.0.0-light 
```

#### 5、创建带备注标签(推荐) 

```
git tag -a 1.0.0 -m "这是备注信息" 
```

#### 6、针对特定 `commit` 版本 `SHA` 创建标签 

```
git tag -a 1.0.0 0c3b62d -m "这是备注信息" 
```

#### 7、删除标签(本地) 

```
git tag -d 1.0.0 
```

#### 8、将本地所有标签发布到远程仓库

```
git push origin --tags 
```

#### 9、指定版本发送 

```
git push origin 1.0.0 
```

#### 10、删除远程仓库对应标签（Git版本 > V1.7.0）

```
git push origin --delete 1.0.0 
```

#### 11、旧版本Git 

```
git push origin :refs/tags/1.0.0
```

#### 12、获取远程标签

```
git fetch origin tag "标签名称"
```

