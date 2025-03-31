---
title: "Automatizované nasazování aplikací"
date: 2024-11-18
author: "Cloud4You"
description: "V rámci tohoto projektu jsme u zákazníka nasadili platformu OpenShift, která poskytuje podporu více aplikačních prostředí v rámci jednoho clusteru. Implementovali jsme GitOps přístup pro Continuous Deployment (CD) pipeline a onboarding projektů prostřednictvím Git, ArgoCD a Helm chartů. Cílem bylo vytvořit efektivní, bezpečnou a automatizovanou platformu pro nasazování aplikací."
categories: ["devops"]
tags: ["cloud", "kubernetes", "redhat", "openshift"]
featured_image: "/images/blog/gitops.jpg"   #w:h 1,9:1
---

<!-- {{< toc >}} -->

## Úvod

V rámci tohoto projektu jsme u zákazníka nasadili platformu OpenShift, která poskytuje podporu více aplikačních prostředí v rámci jednoho clusteru. Implementovali jsme GitOps přístup pro Continuous Deployment (CD) pipeline a onboarding projektů prostřednictvím Git, ArgoCD a Helm chartů. Cílem bylo vytvořit efektivní, bezpečnou a automatizovanou platformu pro nasazování aplikací.

## Výzvy a požadavky zákazníka

Zákazník požadoval robustní platformu pro provoz více oddělených aplikačních prostředí s možností efektivního a automatizovaného nasazování. Mezi klíčové požadavky patřilo:

* Automatizované nasazování aplikací a infrastruktury pomocí GitOps.
* Využití ArgoCD pro správu deklarativních deploymentů.
* Možnost onboardingu nových projektů výhradně prostřednictvím Git repozitáře.
* Správa konfigurací aplikací a infrastruktury pomocí Helm chartů.

## Implementace

### Nasazení OpenShift

Pro efektivní správu více aplikačních prostředí jsme zvolili OpenShift, kde každý tým získal vlastní namespace s definovanými rolemi a oprávněními.

### GitOps pro automatizaci nasazování

Continuous Deployment (CD) pipeline jsme postavili na GitOps přístupu:

* Kód infrastruktury a konfigurace aplikací byl verzován v Git repozitáři.
* ArgoCD monitorovalo změny a automaticky synchronizovalo požadovaný stav s běžícím clusterem.

### Onboarding nových projektů a aplikací

Pro onboarding nových projektů jsme vytvořili centralizovaný Git repozitář obsahující:

* Šablony pro nové projekty.
* Standardizované Helm charty pro nasazování aplikací.
* Politiky pro správu přístupů a bezpečnostní pravidla.

### ArgoCD a Helm charts pro deploymenty

Nasazování aplikací probíhalo deklarativně:

* Každý projekt měl vlastní Helm chart definující aplikační stack.
* ArgoCD sledovalo změny v repozitáři a automaticky provádělo deployment.
* Rollbacky a verzování aplikací byly řešeny přes Git historii.

## Výsledky a přínosy

Nasazené řešení přineslo zákazníkovi několik klíčových výhod:

* __Automatizace__ – eliminace manuálních zásahů při nasazování aplikací.
* __Konzistence__ – všechny deploymenty a konfigurace byly uloženy v Gitu.
* __Bezpečnost__ – striktní řízení přístupů k jednotlivým projektům a prostředím.
* __Jednodušší onboarding__ – nové projekty bylo možné zavádět rychle a konzistentně.
* __Řízené nasasování releasu__ - každý release bylo možné řídit na úrovni Git a nastaveného schvalovacího flow.

## Závěr

Nasazení OpenShift s GitOps přístupem ukázalo, jak lze efektivně a bezpečně provozovat komplexní IT infrastrukturu. Díky využití ArgoCD a Helm chartů jsme dosáhli vysoké úrovně automatizace a stability nasazení. Tento přístup umožnil zákazníkovi snadno spravovat a škálovat své aplikace bez zbytečné provozní zátěže.