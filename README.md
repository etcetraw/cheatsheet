# cheatsheet

Convert a jobject to ContentItem.
```
                if (obj is JObject jObject)
                {
                    contentItem = jObject.ToObject<ContentItem>();
                }
```
Migrations
```
        public int Create()
        {
            _contentDefinitionManager.AlterPartDefinition("Item", part => part
                .WithField("ItemImage", cfg => cfg.OfType("MediaField").WithDisplayName("Main image"))
                .WithField("Price", cfg => cfg.OfType("NumericField").WithDisplayName("Price"))
                .WithField("FromDate", cfg => cfg.OfType("DateField").WithDisplayName("From"))
                .WithField("ToDate", cfg => cfg.OfType("DateField").WithDisplayName("Till"))
                .WithField("Special", cfg => cfg.OfType("BooleanField").WithDisplayName("Special")));


            _contentDefinitionManager.AlterTypeDefinition("Item", menu => menu
                .Draftable()
                .Versionable()
                .Creatable()
                .Securable()
                .WithPart("TitlePart", part => part.WithPosition("1"))
                .WithPart("AutoRoutePart", part => part.WithPosition("2").WithSettings(new AliasPartSettings { Pattern = "{{ ContentItem | display_text | slugify }}" }))
                .WithPart("AliasPart", part => part.WithPosition("3").WithSettings(new AliasPartSettings { Pattern = "{{ ContentItem | display_text | slugify }}" }))
                .WithPart("HtmlBodyPart", part => part.WithPosition("3").WithSettings(new HtmlBodyPartSettings { Editor = "Wysiwig" }))
                .WithPart("Item", part => part.WithPosition("5"))
            );
            _contentDefinitionManager.AlterTypeDefinition("ItemsList", menu => menu
              .Draftable()
              .Versionable()
              .Creatable()
              .Listable()
              .WithPart("TitlePart", part => part.WithPosition("1"))
              .WithPart("AutoRoutePart", part => part.WithPosition("2").WithSettings(new AliasPartSettings { Pattern = "{{ ContentItem | display_text | slugify }}" }))
              .WithPart("AliasPart", part => part.WithPosition("3").WithSettings(new AliasPartSettings { Pattern = "{{ ContentItem | display_text | slugify }}" }))
                .WithPart("HtmlBodyPart", part => part.WithPosition("3").WithSettings(new HtmlBodyPartSettings { Editor = "Wysiwig" }))
              .WithPart("ListPart", part => part.WithPosition("5").WithSetting("ContainedContentTypes", new string[] { "Item" }))
              );

            return 1;
        }
```
