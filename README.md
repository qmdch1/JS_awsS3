# Select Bucket List
```
npm i @aws-sdk/client-s3
```
```
// S3 설정
const accessKeyId = "accesskey";
const secretAccessKey = "secretkey";
const region = "ap-northeast-2";

// 설정란
const Bucket = "bucketname";

const s3Client = new S3Client({ region, credentials: { accessKeyId, secretAccessKey } });
const listObjectsCommand = new ListObjectsV2Command({ Bucket });

s3Client.send(listObjectsCommand)
.then((response) => {
    for(let i=1; i<response.Contents.length; i++){
        key = response.Contents[i].Key;
    }
    res.send(response.Contents);
})
.catch((error) => {
    console.error("Error listing objects:", error);
    res.send(error);
});
```
위 소스의 response.Contents의 key를 조회하면 파일명, 폴더경로 등을 얻을수 있다.

key뿐만 아니라 size, owner, LastModified 등이 있으니 필요한걸 쓰면 되겠다.
