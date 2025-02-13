# Describe an Amazon Rekognition collection using an AWS SDK<a name="example_rekognition_DescribeCollection_section"></a>

The following code examples show how to describe an Amazon Rekognition collection\.

For more information, see [Describing a collection](https://docs.aws.amazon.com/rekognition/latest/dg/describe-collection-procedure.html)\.

------
#### [ \.NET ]

**AWS SDK for \.NET**  
  

```
        public static async Task Main()
        {
            var rekognitionClient = new AmazonRekognitionClient();

            string collectionId = "MyCollection";
            Console.WriteLine($"Describing collection: {collectionId}");

            var describeCollectionRequest = new DescribeCollectionRequest()
            {
                CollectionId = collectionId,
            };

            var describeCollectionResponse = await rekognitionClient.DescribeCollectionAsync(describeCollectionRequest);
            Console.WriteLine($"Collection ARN: {describeCollectionResponse.CollectionARN}");
            Console.WriteLine($"Face count: {describeCollectionResponse.FaceCount}");
            Console.WriteLine($"Face model version: {describeCollectionResponse.FaceModelVersion}");
            Console.WriteLine($"Created: {describeCollectionResponse.CreationTimestamp}");
        }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/dotnetv3/Rekognition/#code-examples)\. 
+  For API details, see [DescribeCollection](https://docs.aws.amazon.com/goto/DotNetSDKV3/rekognition-2016-06-27/DescribeCollection) in *AWS SDK for \.NET API Reference*\. 

------
#### [ Java ]

**SDK for Java 2\.x**  
  

```
    public static void describeColl(RekognitionClient rekClient, String collectionName) {

    try {

        DescribeCollectionRequest describeCollectionRequest = DescribeCollectionRequest.builder()
             .collectionId(collectionName)
             .build();

        DescribeCollectionResponse describeCollectionResponse = rekClient.describeCollection(describeCollectionRequest);

         System.out.println("Collection Arn : " +
             describeCollectionResponse.collectionARN());
         System.out.println("Created : " +
             describeCollectionResponse.creationTimestamp().toString());

    } catch(RekognitionException e) {
        System.out.println(e.getMessage());
        System.exit(1);
    }
   }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javav2/example_code/rekognition/#readme)\. 
+  For API details, see [DescribeCollection](https://docs.aws.amazon.com/goto/SdkForJavaV2/rekognition-2016-06-27/DescribeCollection) in *AWS SDK for Java 2\.x API Reference*\. 

------
#### [ Kotlin ]

**SDK for Kotlin**  
This is prerelease documentation for a feature in preview release\. It is subject to change\.
  

```
suspend fun describeColl(collectionName: String) {

     val request = DescribeCollectionRequest {
            collectionId = collectionName
     }

    RekognitionClient { region = "us-east-1" }.use { rekClient ->
        val response = rekClient.describeCollection(request)
        println("The collection Arn is ${response.collectionArn}" )
        println("The collection contains this many faces ${response.faceCount}")
    }
}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/kotlin/services/rekognition#code-examples)\. 
+  For API details, see [DescribeCollection](https://github.com/awslabs/aws-sdk-kotlin#generating-api-documentation) in *AWS SDK for Kotlin API reference*\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
class RekognitionCollection:
    """
    Encapsulates an Amazon Rekognition collection. This class is a thin wrapper
    around parts of the Boto3 Amazon Rekognition API.
    """
    def __init__(self, collection, rekognition_client):
        """
        Initializes a collection object.

        :param collection: Collection data in the format returned by a call to
                           create_collection.
        :param rekognition_client: A Boto3 Rekognition client.
        """
        self.collection_id = collection['CollectionId']
        self.collection_arn, self.face_count, self.created = self._unpack_collection(
            collection)
        self.rekognition_client = rekognition_client

    @staticmethod
    def _unpack_collection(collection):
        """
        Unpacks optional parts of a collection that can be returned by
        describe_collection.

        :param collection: The collection data.
        :return: A tuple of the data in the collection.
        """
        return (
            collection.get('CollectionArn'),
            collection.get('FaceCount', 0),
            collection.get('CreationTimestamp'))

    def describe_collection(self):
        """
        Gets data about the collection from the Amazon Rekognition service.

        :return: The collection rendered as a dict.
        """
        try:
            response = self.rekognition_client.describe_collection(
                CollectionId=self.collection_id)
            # Work around capitalization of Arn vs. ARN
            response['CollectionArn'] = response.get('CollectionARN')
            (self.collection_arn, self.face_count,
             self.created) = self._unpack_collection(response)
            logger.info("Got data for collection %s.", self.collection_id)
        except ClientError:
            logger.exception("Couldn't get data for collection %s.", self.collection_id)
            raise
        else:
            return self.to_dict()
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/rekognition#code-examples)\. 
+  For API details, see [DescribeCollection](https://docs.aws.amazon.com/goto/boto3/rekognition-2016-06-27/DescribeCollection) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using Rekognition with an AWS SDK](sdk-general-information-section.md)\.