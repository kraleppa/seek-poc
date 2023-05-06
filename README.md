# seek-poc
In this repo, I made a small POC for new a seek implementation using the [Bumblebee](https://github.com/elixir-nx/bumblebee) library. I've tried to fine-tune two existing image classification models for the following case:

During a festival, a bunch of users can download a mobile application with the description of `N` number of unique artifacts, like a rubber duck, painting, plant, etc hidden in the localization of the festival.

Users have to find them and photograph them via a mobile app, which sends an image to some kind of API that checks if one of these artifacts was photographed

Before the festival, the organizers will have to make plenty of photos of each artifact to fine-tune the neural network

To sum up. We need some kind of API that receives an image and may return (assuming that `N = 3`):

- `artifact1-id`
- `artifact2-id`
- `artifact3-id`
- `nil`

## How to run it?
1. Install [Livebook](https://livebook.dev/)
2. Clone this repo
3. Open `.livemd` file in Livebook
4. You'll probably have to change path to the `dataset` (my Livebook setup is quite bizzare :d)

## How the experiments were conducted?

I picked 5 random objects from my flat and made 26 photos of them. Then I rescaled them and sorted them into specific directories. Here are the artifacts:

<p align="center">
  <img width="30%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/0/IMG_3600.jpg"> </img>
  <img width="30%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/1/IMG_3548.jpg"> </img>
  <img width="30%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/2/IMG_3522.jpg"></img>
</p>
<p align="center">
  <img width="30%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/3/IMG_3574.jpg"> </img>
  <img width="30%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/4/IMG_3626.jpg"></img>
</p>

I used two neural networks from HuggingFace:
- [microsoft/resnet-50](https://huggingface.co/microsoft/resnet-50)
- [facebook/convnext-tiny-224](https://huggingface.co/facebook/convnext-tiny-224)

I tried to follow guides from the Bumblebee repository, especially [this one](https://github.com/elixir-nx/bumblebee/blob/main/notebooks/fine_tuning.livemd)

## Conclusions

On my laptop training time of each model was around 4 minutes

### microsoft/resnet-50
As you can see in the notebook accuracy on the training data was 36% which is quite low. However, I was playing around with this model for a while and before I figure out how to persist cell output in Livebook, I got 90% accuracy.

Unfortunately, when I was testing it manually it came up that the network wasn’t really certain about its predictions. Take a look at these examples:

When I gave a network some random image the predictions for each artifact was around 25% which is expected
<img width="60%" src="https://user-images.githubusercontent.com/56135216/236587796-046dbee4-c6a1-4277-a298-621c0b38a1bd.png"></img>

The thing is that in the case when I uploaded an image from the test data set I got the following estimates:
<img width="60%" src="https://user-images.githubusercontent.com/56135216/236587802-ada445f6-2106-4f35-9f37-e23396be62e3.png"></img>

So it seems that the network was guessing correctly, but with extremely low certain level. It's not good for us since we need to detect a case when user uploads an image that does not include any artifact

I couldn't do better with this network so I decided to swtich to something else

### facebook/convnext-tiny-224

In the notebook accuracy on the training data was 100% and it seems to be repeatable. The network is also quite certain about its predictions and reacts properly for an image without actual artifact, so I guess we can call it a success for now

<p align="center">
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588140-45ee542c-da46-4d48-bced-77dcacbba585.png"> </img>
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588159-d0ade2d2-9d77-45b8-a5b9-61824e0734c6.png"> </img>
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588182-154f41e9-6f6f-4cc0-8505-aef39cf3b041.png"></img>
</p>
<p align="center">
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588189-d0d53541-6a4c-4d0f-9945-ef7c30162bef.png"> </img>
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588197-78b9bf76-81e1-4e8e-a237-523ddd5bfe92.png"></img>
  <img width="30%" src="https://user-images.githubusercontent.com/56135216/236588202-334fb055-aba6-4671-96c4-b1276512bcea.png"></img>
</p>





