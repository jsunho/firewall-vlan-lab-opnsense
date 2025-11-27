## Introduction

This project documents the creation of a fully isolated network lab using OPNsense, UTM, and multiple virtual networks running on an Apple Silicon (M1) system. The goal of the lab is to replicate a realistic small-business network environment, complete with segmentation, routing, firewall policies, DHCP, DNS, and controlled access paths.
The lab provides two internal networks — a trusted LAN and an isolated GUEST segment — both routed and filtered through an OPNsense firewall running in an emulated x86_64 virtual machine. Two Linux client VMs are used to verify connectivity, segmentation, and rule enforcement.

## Purpose of the Lab

- Designing layered network architectures

- Implementing segmentation using VLAN-like structures

- Configuring and administering firewall rules in OPNsense

- Working with virtualized environments on Apple Silicon

- Testing and troubleshooting routing, DNS, and DHCP

- Documenting infrastructure in a reproducible way

- These are core skills found in real-world IT 
infrastructure and small-to-medium business environments.

## Why OPNsense + UTM

OPNsense provides an enterprise-grade firewall and routing environment with clear rule structures and predictable behavior.
UTM allows isolated virtual networks on macOS without modifying the host system, making it ideal for experimentation and learning.
Because OPNsense currently requires x86_64 emulation on Apple Silicon, the environment also introduces an additional layer of technical understanding about performance, compatibility, and virtual hardware limitations.

## Scope

This documentation follows the project from initial setup to functional verification:
Preparing UTM virtual networks
Installing and configuring OPNsense
Assigning WAN/LAN/GUEST interfaces
Creating two client VMs
Implementing and testing firewall rules
Validating network isolation and access control
By the end of the project, the system behaves like a minimal but realistic multi-network environment with proper segmentation and controlled access.

By the end of the project, the system behaves like a minimal but realistic multi-network environment with proper segmentation and controlled access.