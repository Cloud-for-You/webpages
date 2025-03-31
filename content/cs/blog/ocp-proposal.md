---
title: "OpenShift platforma v hybridním modelu provozu"
# s GitOps: Automatizované nasazování aplikací"
date: 2024-07-25
author: "Cloud4You"
description: "Většina organizací dnes čelí rostoucím požadavkům na flexibilitu a výkon IT infrastruktury. Hybridní model provozu OpenShift platformy, kde jsou worker nody nasazeny jak na virtuálních serverech, tak na fyzických serverech (baremetal), představuje efektivní řešení. Tento model umožňuje kombinaci výhod obou prostředí: flexibilitu a snadnou správu virtuálních strojů spolu s vysokým výkonem a efektivitou baremetal serverů."
categories: ["containers"]
tags: ["cloud", "kubernetes", "redhat", "openshift"]
featured_image: "/images/blog/ocp.jpg"   #w:h 1,9:1
---

<!-- {{< toc >}} -->

## Úvod

Většina organizací dnes čelí rostoucím požadavkům na flexibilitu a výkon IT infrastruktury. Hybridní model provozu OpenShift platformy, kde jsou worker nody nasazeny jak na virtuálních serverech, tak na fyzických serverech (baremetal), představuje efektivní řešení. Tento model umožňuje kombinaci výhod obou prostředí: flexibilitu a snadnou správu virtuálních strojů spolu s vysokým výkonem a efektivitou baremetal serverů.

## Cíle a přínosy hybridního modelu

### Klíčové cíle

* Optimalizace nákladů na provoz infrastruktury.
* Zajištění výkonu pro náročné workloady (AI/ML) se zachováním flexibilního škálování clusteru.
* Flexibilita v nasazování a škálování workloadů.
* Snadnější rozšiřitelnost a kompatibilita s existujícími IT systémy.

### Přínosy hybridního modelu

* __Výkon:__ Baremetal workery poskytují lepší výkon pro aplikace, které potřebují přímý přístup k hardwaru.
* __Škálovatelnost:__ Virtuální stroje umožňují rychlou reakci na změny v požadavcích na výpočetní kapacitu.
* __Optimalizace nákladů:__ Možnost kombinace dražších, ale výkonnějších baremetal workerů osazených výkonými grafickými kartami s flexibilnějším škálováním celého clusteru pomocí virtuálních workerů.

## Architektura hybridního OpenShift clusteru

### Struktura clusteru

* __Control plane:__ Běží na virtuálních serverech pro snadnou správu a redundanci.
* __Worker nody:__
  * __Virtuální servery:__ Určené pro standardní workloady a mikroservisové aplikace.
  * __Baremetal servery:__ Používané pro aplikace s vysokými požadavky na výkon.

### Integrace s existující infrastrukturou

* Propojení s existující virtualizační platformou (VMware).
* Automatizace provisioning clusteru pomocí Infrastructure-as-Code (Ansible).

## Implementace a provoz

### Nasazení hybridního clusteru

* __Plánování:__ Definice workloadů a rozhodnutí, které aplikace poběží na kterých nodech.
* __Instalace OpenShiftu:__ Použití OpenShift Installeru a nasazení podle našeho návrhu, který je plně automatizován.
* __Konfigurace:__
  * Nastavení podmínek pro scheduling workloadů (node affinity, tolerations).
  * Optimalizace síťové komunikace mezi virtuálními a baremetal workery.
* __Monitoring a observabilita:__
  * Použití Prometheus, Grafana a OpenTelemetry pro sledování výkonu a stavu clusteru.
  * Log management pomocí OpenShift Logging stacku s využitím ECK Cloud deployovaný v onprem prostředí.

## Závěr

Hybridní model provozu OpenShiftu kombinuje flexibilitu a nákladovou efektivitu virtuálních serverů s vysokým výkonem baremetal workerů. Tento přístup poskytuje ideální řešení pro náročné workloady, které potřebují škálovatelnou a efektivní platformu pro moderní aplikace s využíváním AI/ML.
