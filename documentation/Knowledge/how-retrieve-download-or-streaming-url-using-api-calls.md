---
layout: page
title: "How to retrieve the download or streaming URL using API calls?"
date: 2011-12-18 16:23:56
---

The Kaltura Player abstracts the need to retrieve direct access to the video file, and handles the various aspects of the video playback including multi-bitrate, choosing the correct codec and streaming protocols, DRM, Access Control and more. Often applications need a direct URL for downloading the raw media file for purposes such as streaming outside of the Kaltura Player, processing the video data (such as video analysis or transcriptions) and more. In cases where you need to access the playback stream directly, or just a link to download the video file, you will need to consider the target playback devices, any security protocols applied to your Kaltura account and video, and then call the suitable API methods. The following will guide developers of using the playManifest API call to retrieve specific transcoded video flavors from a Kaltura account. 

<p class="mce-heading-2">
  The playManifest API
</p>

The playManifest is a redirect action [<a href="%20https://github.com/kaltura/server/blob/master/alpha/apps/kaltura/modules/extwidget/actions/playManifestAction.class.php" target="_blank">source code</a>], its purpose is to direct media player applications to the desired video stream.

playManifest features return two types:

1.  A redirect to video file for <a href="http://en.wikipedia.org/wiki/Progressive_download" target="_blank">progressive download</a>, or an M3U8 stream descriptor for <a href="http://en.wikipedia.org/wiki/HTTP_Live_Streaming" target="_blank">Apple HTTP Streaming, aka HLS</a>.
2.  An XML response in the form of <a href="http://osmf.org/dev/osmf/specpdfs/FlashMediaManifestFileFormatSpecification.pdf" target="_blank">Flash Media Manifest File</a>.

<p class="mce-heading-3">
  <span>Retrieving a URL for a Video Stream</span>
</p>

To retrieve a specific video flavor, call the **playManifest** API. Be certain to have the Partner ID and Entry ID at hand. To call the **playManifest** API and retrieve a specific video flavor, call the following URL -

**[serviceUrl]**/p/**[YourPartnerId]**/sp/0/playManifest/entryId/**[YourEntryId]**/format/**[StreamingFormat]**/protocol/**[Protocol]**/flavorParamId/**[VideoFlavorId]**/ks/**[ks]**/video.**[ext]**

Replace the following parameters:

*   **serviceUrl - **the base URL to the Kaltura Server (e.g. http://www.kaltura.com)
*   **YourPartnerId** - Your Kaltura account publisher Id. (Can be retrieved from the <a href="http://www.kaltura.com/index.php/kmc/kmc4#account|integration" target="_blank">Publisher Account Settings</a> page in the KMC).
*   ****YourEntryId**** - The Id of the media entry you'd like to retrieve.
*   **StreamingFormat** - See the list of available formats in the table below. This parameter is optional and defaults to <span style="font-family: 'andale mono', times;">/format/url</span>
*   **Protocol** - Whether video is to be delivered over HTTP or HTTPS. See the list of available protocols below for additional options. This parameter is optional and defaults to <span style="font-family: 'andale mono', times;">/format/http</span>
*   ******VideoFlavorId** - ****The Id of the video flavor you want to download. If supported by the streaming format, multiple flavors may be comma-separated.
*   **ks** - A valid Kaltura Session. This parameter is only required when the media entry has an Access Control defined to limit anonymous access to the media.
*   ********ext****** - The file extension of the video you wish to retrieve (For example, mp4, if the video flavor is an MPEG4 file or flv, if the video flavor is an FLV file.)**

** **

<div>
  <p>
    <strong>Available Playback Formats</strong>
  </p>
  
  <table style="width: 787px;" border="1" cellspacing="0" cellpadding="0">
    <tbody>
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            <strong>Format</strong>
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            <strong>Description</strong>
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            mpegdash  
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            MPEG-DASH Streaming.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            applehttp  
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            HTTP Live Streaming (HLS) Streaming.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            url 
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Progressive download.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            hds 
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Adobe HTTP Dynamic Streaming. <em>Not available for all Kaltura accounts.</em>
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            rtmp
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Real Time Messaging Protocol (RTMP). Recommended only for Live, or special use cases.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            rtsp 
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Real Time Streaming Protocol (RTSP). For legacy devices, such as older Blackberry and Nokia phones.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            hdnetworkmanifest
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Akamai HDS delivery. <em>Available only for accounts with Akamai delivery.</em>
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            hdnetwork  
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            Akamai Proprietary Delivery Protocol. <em>Available only for accounts with Akamai delivery.</em> <strong>(deprecated)</strong>
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  
  <p>
    <strong> </strong>
  </p>
  
  <p>
    <strong>Available Protocol Parameters</strong>
  </p>
  
  <table style="width: 787px;" border="1" cellspacing="0" cellpadding="0">
    <tbody>
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            <strong>Protocol</strong>
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            <strong>Description</strong>
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            http
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            http Redirect and streaming URLs make use of the HTTP protocol. (Default)
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            https
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            https  Redirect and streaming URLs make use of the HTTPS protocol.
          </p>
        </td>
      </tr>
      
      <tr>
        <td style="text-align: left;" valign="top" width="135">
          <p>
            rtmp|rtmpe|rtmpt|rtmpte
          </p>
        </td>
        
        <td style="text-align: left;" valign="top" width="653">
          <p>
            (RTMP Streaming only) Streaming Server Base URL make use of the specified protocol (RTMP, RTMPE, RTMPT, or RTMPTE).
          </p>
        </td>
      </tr>
    </tbody>
  </table>
</div>

<div>
  <div>
     
  </div>
  
  <div>
    Examples:
  </div>
  
  <div>
    <ul>
      <li>
        <a href="http://www.kaltura.com/p/309/sp/0/playManifest/entryId/1_rcit0qgs/format/url/flavorParamId/301971/video.mp4">http://www.kaltura.com/p/309/sp/0/playManifest/entryId/1_rcit0qgs/format/url/flavorParamId/301971/video.mp4</a>
      </li>
      <li>
        <a href="http://www.kaltura.com/p/309/sp/0/playManifest/entryId/1_rcit0qgs/format/applehttp/protocol/http/flavorParamId/301971/video.mp4">http://www.kaltura.com/p/309/sp/0/playManifest/entryId/1_rcit0qgs/format/applehttp/protocol/http/flavorParamId/301971/video.mp4</a>
      </li>
    </ul>
  </div>
</div>

<p class="mce-note-graphic">
   
</p>

<p class="mce-note-graphic">
  The playManifest API is not a standard part of the Kaltura API v3, it is a direct URL request that retrieves the specific binary video file from Kaltura. The response to the playManifest URL is the actual video file of the requested entry flavor.<br />The playManifest API does not require a KS unless the media entries were specifically setup with Access Control profiles to limit anonymous access to the media. If the media entry does have Access Control profiles assigned, a KS (Kaltura Session) must be specfied when calling the playManifest URL.
</p>

<p class="mce-heading-2 mce-heading-3">
  <a name="acl-entitlements-consider"></a>Considerations of Access Control and Entitlements
</p>

It is important to note that Kaltura entries can be set for private or protected modes, where access is only allowed when providing a valid admin [Kaltura Session][1].

 [1]: http://knowledge.kaltura.com/faq/how-create-kaltura-session

<p class="mce-procedure">
  For best practice, to retrieve the download URL for an entry, use the following steps:
</p>

1.  Locate the Id of the desired video flavor (see below Video Flavor Id).
2.  Call the <span>flavorAsset</span><span>.</span><span><span class="code-php-call-func"><span class="code-php-func-name">geturl API action.</span></span></span>

<span><span class="code-php-call-func"><span class="code-php-func-name">Below is a PHP code sample for retrieving the download URL of a web-playable flavor for a desired entry Id:</span></span></span>

<pre class="brush: php;fontsize: 100; first-line: 1; ">//Client library configuration and instantiation...

//when creating the Kaltura Session it is important to specify that this KS should bypass entitlemets restrictions:
$ks = $client-&gt;session-&gt;start($secret, $userId, KalturaSessionType::ADMIN, $partnerId, 86400, 'disableentitlement');
$client-&gt;setKs($ks);

$client-&gt;startMultiRequest();
$entryId = '1_u7aj9kasw'; //replace this with your entry Id
$client-&gt;flavorAsset-&gt;getwebplayablebyentryid($entryId);
$req1ResultFlavorId = '{1:result:0:id}'; //get the first flavor from the result of getwebplayablebyentryid
$client-&gt;flavorAsset-&gt;geturl($req1ResultFlavorId); //this action will return a valid download URL
$multiRequestResults = $client-&gt;doMultiRequest();
$downloadUrl = $multiRequestResults[1];
echo 'The entry download URL is: '.$downloadUrl;</pre>

<span class="mce-heading-3">Video Flavor Id</span>

The VideoFlavorId parameter determines which video flavor the API will return as download. This parameter has various options, depending on the Kaltura server deployment and publisher account.

The following lists few of the conventional flavor Id's:

<p class="mce-note-graphic">
  Note: Only flavor id 0 (zero) is static and the same across Kaltura editions. The following list are common flavor Ids on the Kaltura SaaS edition, but note flavors change and upgraded often (improved quality, new codecs, etc.) - Use this list for example purposes.
</p>

*   The original uploaded video (before transcoding) = 0

*   iPhone / Android (mp4) = 301951

*   iPad (mp4) = 301971

*   Nokia/Blackberry (3gp) = 301991

*   Other devices (mp4) = 301961

<p class="mce-procedure">
  The correct flavor Ids (per account and Kaltura edition) can be retrieved by:
</p>

1.  Visiting the KMC Settings > [Transcoding Profiles][2].
2.  OR by making an API call the <a href="https://developer.kaltura.com/api-docs/#/conversionProfile.list" target="_blank">ConversionProfile.list</a> action.

 [2]: http://knowledge.kaltura.com/faq/how-create-transcoding-profile

<p class="mce-heading-3">
  <span>Retrieving Streaming URL for Mobile Applications</span>
</p>

To retrive streaming URL for mobile applications, use the following guidelines:

<p class="p1">
  For Apple iPad devices – <a href="#acl-entitlements-consider">get all the flavors</a> (marked ready) that have the tag 'ipadnew' and build the following URL:
</p>

<pre class="brush: jscript;fontsize: 100; first-line: 1; ">serviceUrl + '/p/' + partnerId + '/sp/' + partnerId + '00/playManifest/entryId/' + entryId + '/flavorIds/' + flavorIds.join(',') + '/format/applehttp/protocol/http/a.m3u8?ks=' + ks + '&referrer=' + base64_encode(application_name)</pre>

<p class="p1">
  For Apple iPhone devices – <a href="#acl-entitlements-consider">get all the flavors</a> (marked ready) that have the tag 'iphonenew' tag and build the following URL:
</p>

<pre class="brush: jscript;fontsize: 100; first-line: 1; ">serviceUrl + '/p/' + partnerId + '/sp/' + partnerId + '00/playManifest/entryId/' + entryId + '/flavorIds/' + flavorIds.join(',') + '/format/applehttp/protocol/http/a.m3u8?ks=' + ks + '&referrer=' + base64_encode(application_name)</pre>

<p class="p1">
  For Android devices that support HLS – <a href="#acl-entitlements-consider">get all the flavors</a> (marked ready) that have the tag 'iphonenew' tag (excluding audio-only flavors where width, height & framerate fields equal to zero) and build the following URL:
</p>

<pre class="brush: jscript;fontsize: 100; first-line: 1; ">serviceUrl + '/p/' + partnerId + '/sp/' + partnerId + '00/playManifest/entryId/' + entryId + '/flavorIds/' + flavorIds.join(',') + '/format/applehttp/protocol/http/a.m3u8?ks=' + ks + '&referrer=' + base64_encode(application_name)</pre>

<p class="p1">
  For Android devices that do not support HLS – get a single video flavor that has the 'iPhoneNew' tag and build the following URL:
</p>

<pre class="brush: jscript;fontsize: 100; first-line: 1; ">serviceUrl + '/p/' + partnerId + '/sp/' + partnerId + '00/playManifest/entryId/' + entryId + '/flavorId/' + flavorId + '/format/url/protocol/http/a.mp4?ks=' + ks + '&referrer=' + base64_encode(application_name)</pre>

<p class="mce-heading-2">
  Retriving the currently playing video URL using the Player JS API
</p>

To retrieve the URL of the video that is being played in the player, use the following player call:

### <a href="http://player.kaltura.com/kWidget/tests/kWidget.getSources.html" target="_blank">kWidget.getSources</a>

To learn more about the <a href="http://www.kaltura.org/demos/kdp3/docs.html#evaluate" target="_blank">evaluate function</a> and the KDP API, read: [JavaScript API for Kaltura Media Players][3].

 [3]: http://knowledge.kaltura.com/node/53
