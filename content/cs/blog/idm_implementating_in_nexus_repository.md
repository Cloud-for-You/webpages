---
title: "Nexus jako centrální Docker repository v multitenant prostředí"
date: 2023-07-24
author: "Petr Hatoň"
description: "Implementace centrálního idM do Community edition Sonatype Nexus repository."
categories: ["docker"]
tags: ["nexus", "sonatype", "opensource", "idM", "docker"]
featured_image: "/images/blog/blog-5.jpg"
---

<!--{{< toc >}}-->

## Jaká byla výzva

Jelikož Sonatype Nexus ve variantě Community edition umožňuje příhlašování uživatelů spravovaných pouze pomocí LDAP, vypadalo toto řešení jednoduše. Největší problém však vznikl, kdy každé jednotlivé Docker repository pro každý tým bylo potřeba prezentovat na unikátním TCP portu. To mělo za následek, že bylo potřeba nejen řešit samostatné oprávněnní k jednotlivým repository, ale taktéž evidenci každého Docker repository a jeho portu a následně provádět konfigurace na mnoha systémech. Tím jak se dynamicky vytvářely a odebíraly projekty, bylo potřeba udržovat tuto evidenci ale hlavně pružně reagovat na všechny změnykonfigurací vzdálených systémů. Tyto systémy se občas neobešli bez odstávek nebo restartů, které znepříjemňovali používání služby a tím snižovali její kvalitu.

Z toho důvodu byla implementována FE proxy před Sonatype Nexus repository a všechna Docker registry byla přesunuta za jeden jediný port.

Tím se nejen zjednodušila evidence, jelikož se přesunula pouze do interního systému Nexus, ale hlavně nebylo potřeba již jiné konfigurace na okolní infrastruktuře a kompletně se odbourala nutná rekonfigurace ostatních systémů.

Dalším benefitem bylo, že pod jednou adresou se všichni tenanti dokázali jednoduše identifikovat a zachovala se kompletní přístupová oprávnění a jejich správa tak jak bylo požadováno (možnost granulovaně řešit oprávnění na jednotlivá repository a využívat již zavedený idM proces).

## Content Organization

### Directory Structure

Create a logical content hierarchy:

{{< code text "Content Structure" >}}
content/
├── blog/
│   ├── tech/
│   ├── tutorials/
│   └── news/
├── products/
├── about/
└── docs/
{{< /code >}}

### Front Matter Templates

Use archetypes to standardize content:

{{< code yaml "archetypes/blog.md" >}}
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
categories: []
tags: []
featured_image: ""
description: ""
author: ""
---

{{</* toc */>}}

## Introduction

[Your introduction here]

## Main Content

[Your content here]
{{< /code >}}

## Content Types

### Page Bundles

Organize related content together:
- Group images with content
- Manage page resources
- Maintain content hierarchy

### Taxonomies

Create meaningful content relationships:

{{< code toml "config.toml" >}}
[taxonomies]
  category = "categories"
  tag = "tags"
  series = "series"
  author = "authors"
{{< /code >}}

## Content Workflow

### Draft Management

1. **Creating Drafts**
   ```bash
   hugo new blog/my-draft-post.md
   ```

2. **Preview Drafts**
   ```bash
   hugo server -D
   ```

3. **Publishing Content**
   - Update front matter
   - Review content
   - Deploy changes

### Content Updates

Maintain content freshness:

1. **Regular Reviews**
   - Check for outdated information
   - Update screenshots
   - Verify external links

2. **Version Control**
   - Track content changes
   - Collaborate with team
   - Maintain history

## Dynamic Content

### Related Content

{{< code html "layouts/partials/related.html" >}}
{{ $related := .Site.RegularPages.Related . | first 3 }}
{{ with $related }}
  <h3>Related Posts</h3>
  <ul>
    {{ range . }}
      <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
    {{ end }}
  </ul>
{{ end }}
{{< /code >}}

### Content Reuse

Create reusable content snippets:

{{< code html "layouts/shortcodes/notice.html" >}}
<div class="notice notice-{{ .Get 0 }}">
  {{ .Inner | markdownify }}
</div>
{{< /code >}}

## SEO and Metadata

1. **Title Optimization**
2. **Meta Descriptions**
3. **URL Structure**
4. **Image Alt Text**

## Content Backup

### Backup Strategies

1. **Version Control**
   - Git repository
   - Regular commits
   - Remote backups

2. **External Storage**
   - Cloud storage
   - Local backups
   - Asset management

## Conclusion

Good content management practices are essential for maintaining a successful Hugo site. By following these guidelines, you can create an efficient and scalable content workflow.

## Resources

- [Hugo Content Management Documentation](https://gohugo.io/content-management/)
- [Hugo Archetypes Guide](https://gohugo.io/content-management/archetypes/)
- [Hugo Taxonomies Documentation](https://gohugo.io/content-management/taxonomies/)
