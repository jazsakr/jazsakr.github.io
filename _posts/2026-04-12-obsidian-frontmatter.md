---
title: "Using frontmatter in Obsidian notes" 
excerpt: "Add metadata to Obsidian notes using the frontmatter."
date: 2026-04-12
header:
  teaser: /assets/images/posts/2026-04-12-obsidian-frontmatter-thumbnail.png
categories:
  - obsidian
tags:
  - obsidian
  - tutorial
  - tip
---

One of the great things about using Obsidian is the ability to add metadata to your notes using a frontmatter.

# What is a frontmatter?
Frontmatter is where the metadata in [Markdown files](https://markdownlivepreview.com) is written. It is usually at the very top of the page and is written in [YAML](https://yaml.org) (or [JSON](https://www.json.org/)). To add a frontmatter to a Markdown file, on the very first line of the file add three dashes, in the following lines add the metadata you want in YAML syntax, and end the frontmatter by adding another line of three dashes. This results in a three-dashed block at the top of your file. It might look something like this

```yaml
---
title: "Title of the page" 
date: YYYY-MM-DD
tags:
  - tag1
  - tag2
  - tag3
---
```

---

## Obsidian's frontmatter

Obsidian is basically a folder of markdown files (and hidden folders of fancy things that make up the Obsidian functionality and related plug-ins). Obsidian supports these [properties](https://help.obsidian.md/properties) in the [frontmatter of its notes](https://help.obsidian.md/glossary#Frontmatter) (as of March 2026):
- **[Text](https://help.obsidian.md/properties#Text)**
- **[Number](https://help.obsidian.md/properties#Number)**
- **[Checkbox](https://help.obsidian.md/properties#Checkbox)**
- **[List](https://help.obsidian.md/properties#List)**
- **[Date](https://help.obsidian.md/properties#Date)**
- **[Date & time](https://help.obsidian.md/properties#Date%20&%20time)**
- **[Tags](https://help.obsidian.md/properties#Tags)**

Usually frontmatters are hidden in markdown files, but in Obsidian it shows in the notes. Here is an example using a daily note:
![Screenshot of Obsidian frontmatter of a daily note in both editing view and reading view.](/assets/images/posts/2026-04-12-obsidian-frontmatter-editing-reading-view.png)

When switching from editing view (left) to reading view (right), the metadata is still visible. You can add properties by typing them out in editing view or in reading view by clicking "+ Add property" at the bottom of the frontmatter. Notice how there are different icons next to each piece of metadata based on the property type. After adding a new property, you can change the type by clicking on the icon on the left hand side of the property. The current property type will have a check mark next to it.

![Screenshot of Obsidian frontmatter of a daily note in reading view while changing property type of metadata.](/assets/images/posts/2026-04-12-obsidian-frontmatter-reading-view-change-property-annot.png)

---

### Other properties

Obsidian has a few [default properties](https://obsidian.md/help/properties#Default+properties) and these property types cannot be assigned to other properties. One already mentioned is `tags` and the others are `aliases` and `cssclasses`. 

`aliases` are especially useful for things like acronyms and abbreviations. We can use YAML as example. The name "YAML" is a recursive acronym for "[YAML Ain't Markup Language](https://yaml.org/about/#history)". In your vault, using the aliases property will point both `YAML` and `YAML Ain't Markup Language` to the same note which is efficient because now we do not need to create two separate notes for the same thing. Here is what this alias might look like:

```yaml
---
aliases:
  - YAML
  - YAML Ain't Markup Language
---
```

For more information on how Obsidian uses aliases, see the [Obsidian aliases documentation](https://obsidian.md/help/aliases).

---

`cssclasses` lets you customize individual note styles using CSS snippets. For detailed information on CSS snippets, see the [Obsidian CSS snippets documentation](https://obsidian.md/help/snippets).

---

Because these default properties cannot be assigned to other properties, you cannot change this property type. When you click on the icon to try to change the property type, you will not be able to. 

![Screenshot of Obsidian frontmatter of a daily note in reading view while attempting to change property type of default Obsidian metadata.](/assets/images/posts/2026-04-12-obsidian-frontmatter-reading-view-cannot-change-property-annot-crop.png)

---

Although not listed officially as a property type, you could also use nested objects or a dictionary in your frontmatter, which looks something like this:

```yaml
---
object:
  object1:
  object2:
---
```

Although the icon for this property type looks like an error icon, the metadata can be parsed and utilized by Obsidian. To take it one step further, this nested object can be mixed and matched with other property types to create complex and rich metadata:

```yaml
---
object:
  object1: 67
  object2: text
    - object2a: 56
    - object2b: 99
---
```

---

Here is the full example using a daily notes with all the property types mentioned in reading view:

![Screenshot of Obsidian frontmatter of a daily note in reading view with Obsidian metadata.](/assets/images/posts/2026-04-12-obsidian-frontmatter-full-reading-view.png)

# Now what?
Once you have added metatdata to your notes, you now have the ability to parse, search, filter and organize your notes very quickly and efficiently with Obsidian's core features as well as with community plug-ins. For example, you can create dynamic tables and galleries that are automatically updated when you add new notes with the same metadata. Another is example is that if you add metadata to your daily notes, you can visualize activity in a calendar. 


[See an example here](https://jazsakr.github.io/obsidian-phd-vault/activity-tracking/){: .btn .btn--primary}
