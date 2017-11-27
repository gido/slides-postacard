# Postacard

# Me

# The Genesis - it was 2015

    * I wanted to learn NodeJS (back in 2015)
    * I was looking for a sideproject to build


# Postacard.ch
A mix of two products:

    * PostCard Creator (by the Swiss Post)
    * Instagram

## PostCard Creator

 > Produce your post card mailing online with PostCard Creator.

    * [A web app](https://postcardcreator.post.ch)
    * [A mobile app](https://itunes.apple.com/ch/app/postcard-creator/id820354055?mt=8)

> With PostCard Creator, send one free postcard every 24 hours.


## Instagram
Do I need to present this application?


## What is Postacard
Send Instagram photo as a real postcard by just adding a custom hashtag (eq: <code>#postacard</code> or <code>grandma</code>).

Postacard.ch let you map a specific hashtag with a (Postal) Address.

(Postacard will queue the delivery to use the free sending each 24h.)

# How to build it ?

    * Sadly, PostCard Creator don't offer an open API.
    * But an undocumented API exist !

# Reverse Engineering

## Tools

    * Charles Web Debugging Proxy: https://www.charlesproxy.com/
    * or Wireshark (https://www.wireshark.org/)
    * Postman

## Step to send a postcard

1. Authentication <small>(get a JWT token)</small>
2. Fetch your UserID
3. Check Quota (optional)
4. Create a mailing. <small>This return a mailing ID</small>
5. Upload asset (photo). <small>This return an asset ID</small>
6. Set recipient address to created mailing.
7. Send the layout (SVG) of the front page (the photo)
8. Send the layout (SVG) of the back page (the message + recipient address)
9. Create an Order.


# PostCard Creator API demystified
(Look at the [tests](https://github.com/gido/postcardcreator/tree/master/spec) inside the postcardcreator lib).

## Authentication

## Users endpoint

    GET /rest/2.0/users/current
    GET /rest/2.0/users/{userId}

    # POST /rest/2.0/users

## Quota endpoint

    GET /rest/2.0/users/{userId}/quota


## Mailing endpoint

    POST /rest/2.0/users/{userId}/mailings

## Mailing Recipients endpoint

    PUT /rest/2.0/users/{userId}/mailings/{mailingId}/recipients

## Assets endpoint

    POST /rest/2.0/users/{userId}/assets

## Page Layout (front)

    PUT /rest/2.0/users/{userId}/mailings/{mailingId}/pages/1

    Content-Type: image/svg+xml

## Page Layout (Back)

    PUT /rest/2.0/users/{userId}/mailings/{mailingId}/pages/2

    Content-Type: image/svg+xml

## Order Endpoint

    POST /rest/2.0/users/{userId}/mailings/{mailingId}/order

----

# Source

 * Postcardcreator API javascript client: https://github.com/gido/postcardcreator/
 * Postcardcreator python API wrapper (by Andrin Bertschi): https://github.com/abertschi/postcard_creator_wrapper
