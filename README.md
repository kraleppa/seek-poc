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

<img width="33%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/0/IMG_3600.jpg"> </img>
<img width="33%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/1/IMG_3548.jpg"> </img>
<img width="33%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/2/IMG_3522.jpg"></img>
<p align="center">
  <img width="33%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/3/IMG_3574.jpg"> </img>
  <img width="33%" src="https://github.com/kraleppa/seek-poc/blob/main/dataset/4/IMG_3626.jpg"></img>
</p>

I used two neural networks from HuggingFace:
- [microsoft/resnet-50](https://huggingface.co/microsoft/resnet-50)
- [facebook/convnext-tiny-224](https://huggingface.co/facebook/convnext-tiny-224)

You can find more details in notebooks





