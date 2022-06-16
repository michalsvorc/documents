# Youtube (Video Sharing Service)

- [xunhuanfengliuxiang.gitbooks.io](https://xunhuanfengliuxiang.gitbooks.io/system-desing/content/design-youtube.html)

## Functional requirements

- Users should be able to upload videos.
- Users should be able to share and view videos.
- Users can perform searches based on video titles.
- Our services should be able to record stats of videos, e.g., likes/dislikes, total number of views, etc.
- Users should be able to add and view comments on videos.

## Non-functional requirements

Non-Functional Requirements:

- The system should be highly reliable, any video uploaded should not be lost.
- Users should have real time experience while watching videos and should not feel any lag.

## Considerations

- There will be a lot more thumbnails than videos.
- We should segregate our read traffic from write.
- Keeping hot thumbnails in the cache will also help in improving the latencies.
- Our service will have to deal with widespread video duplication.
- We should split user data and video metadata.

## Processing

Encoder: To encode each uploaded video into multiple formats.
Thumbnails generator: We need to have a few thumbnails for each video.
