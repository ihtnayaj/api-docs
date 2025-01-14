## Contact Interactions
<a name="zapier_contact_interactions"></a>

**Summary:** This HIPAA Compliant trigger returns all interactions (or leads) generated by a campaign for an advertiser.

**Contact Interaction Details**

Field | Type | Description
--------- |-------- |--------
id | Integer | An integer uniquely identifying this contact interaction.
contact_id | Integer | An integer uniquely identifying the contact to which this contact interaction belongs.
campaign_id | Integer | An integer uniquely identifying the campaign that this contact interaction is attributed to.
campaign_name |  String| The name of the campaign that this contact interaction is attributed to.
archived_at | Datetime | The date and time which this contact interaction was archived.
created_at | Datetime | The date and time which this contact interaction was created.
important_at | Datetime | The date and time which this contact interaction was marked important.
occured_at | Datetime | The date and time which this contact interaction occurred. This will usually be different than the date that the contact interaction was created.
read_at | Datetime | The date and time which this contact interaction was marked read.
display_name | String | The display name of the contact interaction.
event_type| String | The type of the contact interaction . Valid values are **chat**, **call** and **form**.
status | String | The status of the associated contact.  Valid values are **pending_contact**, **active_contact interaction**, **client** and **none**.
notes | String | Free form text notes entered by end users onto the contact interaction .
tags | Array of String | When present represents a collection of tags use for applying ad-hoc categorization and collation of contact interactions.
contact | Contact | The contact to which this contact interaction belongs.  See the contacts page of this document for details

Depending on the type of contact interaction (see the `event_type` attribute), the payload will also include one of the following:

**Chat**

Field | Nullable | Description
--------- |-------- |--------
summary | String | A freeform text description of the chat.
transcript | Array of ChatTranscripts | An ordered array of chat transcript objects.

**ChatTranscript Object**

Field | Type | Description
--------- |-------- |--------
id | Integer | A sequential id of the line chat transcript.  It uniquely identifies a line of the chat transcript within this contact interaction.
timestamp | Datetime |The date and time that the external chat API registered for this line of the chat transcript.
from | String | The display name of the member of the chat who sent this message.
message | String |The message body of this line of the chat transcript.

**Call**

Field | Type | Description
--------- |-------- |--------
occured_at | Datetime | The date and time that the call occurred.
duration | Integer | The duration of the call in seconds.
recording_url | String | The URL address to an audio recording of the call.

**Form Fill**

Field | Type | Description
--------- | -------- |-------- |--------
sub_type | String | The subtype of the form.  Valid values are **FormPost** and **FormEmail**.
full_message | String | The full form message
subject | String |
extra_fields | Array of String |
