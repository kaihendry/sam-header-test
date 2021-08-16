# header-test

Debugging https://stackoverflow.com/questions/68765603/how-do-you-trace-microservices-with-the-aws-x-ray-sdk-for-go

	curl -s -H "x-amzn-trace-id: foobar"  https://mq32ocs5y9.execute-api.ap-southeast-1.amazonaws.com/Prod/hello/ | grep foobar
	Hello, {/hello /hello/ GET map[Accept:*/* CloudFront-Forwarded-Proto:https CloudFront-Is-Desktop-Viewer:true CloudFront-Is-Mobile-Viewer:false CloudFront-Is-SmartTV-Viewer:false CloudFront-Is-Tablet-Viewer:false CloudFront-Viewer-Country:SG Host:mq32ocs5y9.execute-api.ap-southeast-1.amazonaws.com User-Agent:curl/7.78.0 Via:2.0 6a453f38d14868702eadac9560675990.cloudfront.net (CloudFront) X-Amz-Cf-Id:Npd9iPSoUfLTojwm5bk-aipIDkIaH9-qa9Kf_n7fgU4YNZjjtZhmMg== X-Amzn-Trace-Id:Root=1-6119f456-192f4543005587e217e8e22e;foobar X-Forwarded-For:210.23.22.2, 204.246.166.173 X-Forwarded-Port:443 X-Forwarded-Proto:https] map[Accept:[*/*] CloudFront-Forwarded-Proto:[https] CloudFront-Is-Desktop-Viewer:[true] CloudFront-Is-Mobile-Viewer:[false] CloudFront-Is-SmartTV-Viewer:[false] CloudFront-Is-Tablet-Viewer:[false] CloudFront-Viewer-Country:[SG] Host:[mq32ocs5y9.execute-api.ap-southeast-1.amazonaws.com] User-Agent:[curl/7.78.0] Via:[2.0 6a453f38d14868702eadac9560675990.cloudfront.net (CloudFront)] X-Amz-Cf-Id:[Npd9iPSoUfLTojwm5bk-aipIDkIaH9-qa9Kf_n7fgU4YNZjjtZhmMg==] X-Amzn-Trace-Id:[Root=1-6119f456-192f4543005587e217e8e22e;foobar] X-Forwarded-For:[210.23.22.2, 204.246.166.173] X-Forwarded-Port:[443] X-Forwarded-Proto:[https]] map[] map[] map[] map[] {407461997746 h6hbyx  Prod mq32ocs5y9.execute-api.ap-southeast-1.amazonaws.com mq32ocs5y9 d110bcc5-e9c8-4e69-b9a3-0c36ac465b74 HTTP/1.1 {       210.23.22.2    curl/7.78.0 } /hello map[] GET 16/Aug/2021:05:15:02 +0000 1629090902609 mq32ocs5y9}  false}

Notice the x-amzn-trace-id gets appended!

https://github.com/kaihendry/x-amzn-trace-id silently drops (or overwrites) the set x-amzn-trace-id header
