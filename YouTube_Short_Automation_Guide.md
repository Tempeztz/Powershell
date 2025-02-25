
# Automating YouTube Short Uploads Using Canva, Dropbox, and Make.com

## 1. Create a YouTube Short in Canva
- Open Canva (canva.com) and log in to your account.
- Click on the "Create a Design" button and select **YouTube Shorts** (9:16 aspect ratio).
- Design your Short by adding videos, images, text, or animations.
- Once your design is complete, click on **Download** in the top-right corner.
- Choose your preferred file format (MP4 recommended for video).
- Save the file to your computer.

## 2. Upload Your YouTube Short to Dropbox
- Go to [Dropbox](https://www.dropbox.com) and log in to your account.
- Click on the **Upload** button and select the YouTube Short file you downloaded from Canva.
- Once uploaded, make sure the file is publicly accessible or get the shareable link by right-clicking the file and selecting **Share** > **Create a link**.
- Copy the link to use in Make.com.

## 3. Set Up Make.com to Automate YouTube Uploads
- Log in to your [Make.com](https://www.make.com) account.
- **Create a New Scenario**:
  1. Click on **Create a new scenario**.
  2. Select the **Repeater** module and set it to run every 3 days. This will define the frequency of uploads.
  3. Add the **Dropbox** module and configure it to fetch the video file you uploaded.
     - Choose **Get File** in the Dropbox module.
     - Paste the shareable link of your Dropbox file.
  4. Add the **YouTube** module to upload the video.
     - Choose **Upload Video** in the YouTube module.
     - Connect your YouTube account.
     - Map the Dropbox file to the video upload field in the YouTube module.
     - Set other video properties like title, description, tags, and visibility.
- **Test the Scenario**:
  - Once the scenario is set up, click on **Run Once** to test if everything is working smoothly.
  - Make sure the video is uploaded correctly to your YouTube channel.

## 4. Finalize and Activate the Automation
- Once you've tested the scenario and everything is working, click **Activate** to start the automation.
- Your YouTube Shorts will now be uploaded automatically to your YouTube channel every 3 days from Dropbox.

---

## Summary
This workflow automates the process of creating, uploading, and publishing YouTube Shorts using Canva, Dropbox, and Make.com. By following these steps, you can save time and ensure your content is consistently uploaded to YouTube.
