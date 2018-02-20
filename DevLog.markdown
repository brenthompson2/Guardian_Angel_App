# DevLog

### Development log detailing the daily work done and the references used during the creation of the Guardian Angel Ionic Hybrid Mobile App
### Winter 2018

==================================================================================

## **==================================================**
## **====== 02/20/18 = Brendan Thompson ======**
## **==================================================**

### Summary:
	- Implemented Image Flattening
	- Simplified Data Model

### Need to Implement:
Functionality:

	- Get Images from Firebase
	- Get Texts from Firebase
	- Figure out using Image when sharing

Design:

	- Currently isn't one

BackEnd:

	- Firebase?

### Log of activity

##### Implemented Image Flattening

- Flattened the image in new blank project (flattenTest)
- Implemented that code in Confirm page
- Moved the Canvas to pic-select & text-select pages and only pass the img to Confirm & Final pages

1) Import ElementRef & ViewChild for accessing the Canvas

	import { ElementRef, ViewChild } from '@angular/core';

2) Add ElementRef to constructor

	private elementReference: ElementRef

3) Access the Canvas & create member variables

    @ViewChild('myCanvas') canvasEl: ElementRef;
    private theCanvas: any;
    private theContext: any;
    private finalImage: any;

4) Call the initialization from ionViewDidLoad()

    ionViewDidLoad(){
        this.initialiseCanvas();
    }

5) Initialize the Canvas

    initialiseCanvas(){
        this.theCanvas = this.canvasEl.nativeElement;
        this.theCanvas.width = window.innerWidth;
        this.theCanvas.height = window.innerHeight;
        if(this.theCanvas.getContext){
            this.theContext = this.theCanvas.getContext('2d');
            this.drawTheImage();
        }
    }

6) Draw the Image

    drawTheImage(){
        // Display the Image
        var img = new Image();
        img.setAttribute('crossOrigin', 'anonymous');
        img.onload = (event) => {
            this.theContext.drawImage(img, this.theCanvas.width/2 - img.width/2, this.theCanvas.height/2 - img.height/2);
            this.drawText();
        };
        img.src=this.selectedPicture;
    }

7) Draw the Text

    drawText(){
        this.theContext.strokeStyle = "rgba(256, 0, 0, 1.0)";
        this.theContext.font = "50px Arial";
        this.theContext.textAlign = "center";
        this.theContext.strokeText(this.selectedText.text, this.theCanvas.width/2, this.theCanvas.height/2);
        this.saveCanvas();
    }

8) Set the finalImage given the Canvas

    saveCanvas(){
        this.finalImage = this.theCanvas.toDataURL();
    }

##### Simplified Data Model

- Moved the Canvas to pic-select & text-select pages and only pass the img to Confirm & Final pages

## **==================================================**
## **====== 02/18/18 = Brendan Thompson ======**
## **==================================================**

### Summary:
	- Learned how to use the Canvas
	- Learned how to draw the Image & Text centered on the canvas
	- See canvas-tutorial directory

## **==================================================**
## **====== 02/13/18 = Brendan Thompson ======**
## **==================================================**

### Summary:
	- Implemented Sharing (images not working well)
	- Learned Facebook doesn't allow prefilling the comment when sharing

### Need to Implement:
Functionality:

	- Get Images from Firebase
	- Get Texts from Firebase
	- Flatten the text onto the image
	- Figure out using Image when sharing

Design:

	- Currently isn't one

BackEnd:

	- Firebase?

### Log of activity

##### Started Sharing to Facebook

- https://ionicframework.com/docs/native/facebook/
- https://www.youtube.com/watch?v=tCaj70w26As
- Not allowed to prefill captions, comments, messages, or the user message parameter of posts with content, even if the person can edit or remove the content before sharing.
	- https://developers.facebook.com/policy/#integration

A) Import Social Sharing

	- ionic cordova plugin add cordova-plugin-x-socialsharing
	- npm install --save @ionic-native/social-sharing
	- Import to app.module.ts: import { SocialSharing } from '@ionic-native/social-sharing';
	- Add to list of Providers: SocialSharing

B) Implement Social Sharing in confirm.ts

	- Import to confirm.ts: import { SocialSharing } from '@ionic-native/social-sharing';
	- Add to constructor: public sharing: SocialSharing)

C) Write function to post to Facebook

    shareToFacebook(){
        this.mySharing.shareViaFacebookWithPasteMessageHint("I am sending you this Guardian Angel ", this.selectedPicture.href, null)
            .then(() => {
                console.log("Sent Via Facebook");

            })
            .catch((error) =>{
                console.log(error);
            });
    }


##### Implemented all sorts of sharing possibilities

- https://ionicframework.com/docs/native/social-sharing/
- share()
- shareViaTwitter()
- shareViaInstagram()

## **==================================================**
## **====== 02/08/18 = Brendan Thompson ======**
## **==================================================**

### Summary:
	- Created overall layout of the App
	- Started PicSelectPage & created PictureListProvider
	- Started TextSelectPage & created TextListProvider
	- Started RecipientSelectPage & created RecipientListProvider
	- Started ConfirmPage

### Need to Implement:
Functionality:

	- Get Images from Firebase
	- Get Texts from Firebase
	- Flatten the text onto the image
	- Send the Guardian Angel to someone

Design:

	- Currently isn't one

BackEnd:

	- Firebase?

### Log of activity

##### Started PicSelectPage & Created PictureListProvider

Getting a list from a provider

- How to get data from a provider: [Passing Data Between Pages: Ionic 2, by Satish B](https://www.youtu.be/oJtS8fHR1Co)
	- create loadAll() fn within provider
	  	`loadAll(){
	  		return Promise.resolve(this.pictureList);
	  	}`

	- Get the data in pic-select.ts
		`pictureListProviderObject.loadAll().then(result =>{
  			this.pictureList = result;
  		});`

- How to Get an image to display based on a JSON src: [Stack Overflow](https://stackoverflow.com/questions/43882578/unable-to-use-ng-src-cant-bind-to-ng-src-since-it-isnt-a-known-property)

	<img *ngIf="currentPicture != 0" [attr.src]="currentPicture.href">

##### Started TextSelectPage & Created TextListProvider

##### Started RecipientSelectPage & created RecipientListProvider

##### Started ConfirmPage



## **==================================================**
## **====== 02/07/18 = Brendan Thompson ======**
## **==================================================**

### Summary:
- Created Project and Github Repo
	- Made baby steps on the Project

### Need to Implement:

Functionality:

	- Let the user select an image
		- Get images as an array from a provider
	- Let the user select a text
		- Get texts as an array from a provider
	- Flatten the text onto the image
	- Send the Guardian Angel to someone

Design:

	- Currently isn't one

BackEnd:

	- Firebase?

### Log of activity

Struggled linking git repositories
Removed tabs from app.component.ts & app.module.ts
Started Implementing General Project

	- ID, Name, Description