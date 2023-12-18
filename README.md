
# Sonatype Nexus 3 private npm registry Setup
## npm registry creation


## Realms, Roles and Users
### Realms


### Roles


### Users




## Local machine Setup
### .npmrc
Reference:  
xxxhttps://support.sonatype.com/hc/en-us/articles/115015110067-Usng-User-Tokens-with-npm  
https://help.sonatype.com/repomanager3/nexus-repository-administration/formats/npm-registry/npm-security  


```shell
echo -n '$USERNAME:$PASSWORD' | openssl base64
or
printf '$USERNAME:$PASSWORD' | openssl base64
```

`echo -n` removes the newline which `echo` automatically added to the input string.  
`printf` does not append any newline to the input string.  
Reference:  
https://stackoverflow.com/a/30762067  

```shell
# for example
echo 'admin:admin123' | openssl base64
# YWRtaW46YWRtaW4xMjMK
echo -n 'admin:admin123' | openssl base64
# YWRtaW46YWRtaW4xMjM=
```


There are two ways to configure the `.npmrc` file.  
1. Edit it directly, it usually locates at `~/.npmrc`.  
```shell
registry=$HOSTED_REPOSITORY_URL
$HOSTED_REPOSITORY_URL_WITHOUT_HTTP_COLON:_auth=$BASE64_STRING_PREPARED_BEFORE

# for example, login and password is admin and admin123:
registry=http://localhost:8081/repository/npm-internal/
//localhost:8081/repository/npm-internal/:_auth=YWRtaW46YWRtaW4xMjM=
```


2. Edit it by using `npm config edit` command.  
Put the same content as 1).  


3. Edit it by using `npm config set` command.  
Reference:  
https://stackoverflow.com/a/43012838  

```shell
npm config set registry=$HOSTED_REPOSITORY_URL
npm config set _auth="$(echo -n '$USERNAME:$PASSWORD' | openssl base64)"
```

Finally using `npm config list` to check the content.  







