# cheatsheet

Convert a jobject to ContentItem.
```
                if (obj is JObject jObject)
                {
                    contentItem = jObject.ToObject<ContentItem>();
                }
```
