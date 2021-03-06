---
-api-id: T:Windows.UI.WebUI.WebUIContactVideoCallActivatedEventArgs
-api-type: winrt class
---

<!-- Class syntax.
public class WebUIContactVideoCallActivatedEventArgs : Windows.ApplicationModel.Activation.IActivatedEventArgs, Windows.ApplicationModel.Activation.IContactActivatedEventArgs, Windows.ApplicationModel.Activation.IContactVideoCallActivatedEventArgs, Windows.UI.WebUI.IActivatedEventArgsDeferral
-->

# Windows.UI.WebUI.WebUIContactVideoCallActivatedEventArgs

## -description
Provides data when an app is activated to video call a contact.

## -remarks
This object is accessed when you implement an event handler for the [WinJS.Application.Onactivated](http://msdn.microsoft.com/library/8b1cf913-a914-47d1-a690-bc3f0931e9d4) or the [Windows.UI.WebUI.WebUIApplication.activated](webuiapplication_activated.md) events when [ActivationKind](../windows.applicationmodel.activation/activationkind.md) is **contact**.



> [!NOTE]
> : This class is not agile, which means that you need to consider its threading model and marshaling behavior. For more info, see [Threading and Marshaling (C++/CX)](http://go.microsoft.com/fwlink/p/?linkid=258275).

Windows 8.1 allows users to video call their contacts from the [Contact Card](../windows.applicationmodel.contacts/contactmanager_showcontactcard.md) or Windows Search experience. By implementing the contact video call activation contract, Windows can launch your app to make video calls for the user.

To receive video call activations, your app must register for the "windows.contact" extension category in its manifest. Under this extension, you must include a "LaunchAction" element with the "Verb" attribute equal to "videoCall." You can then specify the "ServiceId" element to specify the domain name of the service that your app can video call over, for example "skype.com."

If multiple apps have registered for this contract, the user can choose one of them as their default for handling video calls.



Here is an example for manifest registration:

```xml

<m2:Extension Category="windows.contact" xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">
  <m2:Contact>
    <m2:ContactLaunchActions>
      <m2:LaunchAction Verb="videoCall" DesiredView="useHalf">
        <m2:ServiceId>skype.com</m2:ServiceId>
      </m2:LaunchAction>
    </m2:ContactLaunchActions>
  </m2:Contact>
</m2:Extension>

```



After you register in your manifest, your app can be activated for the contact video call contract. When your app is activated, you can use the event information to identify the video call activation and extract the parameters that help you complete the video call for the user.

Here is an example of the code you need to handle contact video call activations for Skype Ids:

## -examples
JavaScript

```javascript
function activated(eventObject) {
    if (eventObject.detail.kind === Windows.ApplicationModel.Activation.ActivationKind.contact) {
        if (eventObject.detail.verb === Windows.ApplicationModel.Contacts.ContactLaunchActionVerbs.videoCall) {

     //get contact display info
            var contactName = eventObject.detail.contact.displayName;
            var contactThumbnail = eventObject.detail.contact.thumbnail;

     if (eventObject.detail.serviceId === "skype.com") {
                var userId = eventObject.detail.serviceUserId;
  //add video calling logic for Skype Ids
            }
        }
    }
}

```



## -see-also
[IContactVideoCallActivatedEventArgs](../windows.applicationmodel.activation/icontactvideocallactivatedeventargs.md), [IContactActivatedEventArgs](../windows.applicationmodel.activation/icontactactivatedeventargs.md), [IActivatedEventArgs](../windows.applicationmodel.activation/iactivatedeventargs.md), [IActivatedEventArgsDeferral](iactivatedeventargsdeferral.md), [Handling Contact Actions sample](http://go.microsoft.com/fwlink/p/?LinkID=320151)