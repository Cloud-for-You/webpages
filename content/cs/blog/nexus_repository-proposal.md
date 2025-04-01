---
title: "Artifact repository v multitenant prostředí"
date: 2024-05-12
author: "Petr Hatoň"
description: "Implementace OpenSource Sonatype Nexus repository jako hlavního repozitáře pro verzování releasovaných aplikací a a jako proxy pro získávání nutných knihoven z upstreamu."
categories: ["docker"]
tags: ["nexus", "sonatype", "opensource", "idM", "docker"]
featured_image: "/images/no_image.png"
---

<!--{{< toc >}}-->

## Jaká byla výzva

Jelikož Sonatype Nexus ve variantě Community edition umožňuje příhlašování uživatelů spravovaných pouze pomocí LDAP, vypadalo toto řešení jednoduše. Největší problém však vznikl, kdy každé jednotlivé Docker repository pro každý tým bylo potřeba prezentovat na unikátním TCP portu. To mělo za následek, že bylo potřeba nejen řešit samostatné oprávněnní k jednotlivým repository, ale taktéž evidenci každého Docker repository a jeho portu a následně provádět konfigurace na mnoha systémech. Tím jak se dynamicky vytvářely a odebíraly projekty, bylo potřeba udržovat tuto evidenci ale hlavně pružně reagovat na všechny změnykonfigurací vzdálených systémů. Tyto systémy se občas neobešli bez odstávek nebo restartů, které znepříjemňovali používání služby a tím snižovali její kvalitu.

Z toho důvodu byla implementována FE proxy před Sonatype Nexus repository a všechna Docker registry byla přesunuta za jeden jediný port.

Tím se nejen zjednodušila evidence, jelikož se přesunula pouze do interního systému Nexus, ale hlavně nebylo potřeba již jiné konfigurace na okolní infrastruktuře a kompletně se odbourala nutná rekonfigurace ostatních systémů.

Dalším benefitem bylo, že pod jednou adresou se všichni tenanti dokázali jednoduše identifikovat a zachovala se kompletní přístupová oprávnění a jejich správa tak jak bylo požadováno (možnost granulovaně řešit oprávnění na jednotlivá repository a využívat již zavedený idM proces).


