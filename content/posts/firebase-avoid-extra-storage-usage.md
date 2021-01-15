---
title: "How to avoid excessive Firebase storage"
date: 2021-01-15
categories: [firebase]
tags: [firebase, storage, billing]
description: "If you are using firebase for the first time and you have created some cloud functions, you will notice that eventually you will see a sudden increase in Fire cloud storage"
draft: true
---

## The problem

If you are using firebase for the first time and you have created some cloud functions, you will notice that eventually you will see a sudden increase in Fire cloud storage.

It happened to me after multiple deployments in one day. I noticed that cloud storage was over 2 GB when I only had handful of functions!
[add screenshot].

This was causing a surge in bandwidth as well [explain why and how firebase is transferring these artifacts].

To make it even more annoying, you will not be able to see what is causing this excessive storage. If you navigate to Cloud Storage inside Firebase console, you will see an empty bucket.

## Why this is happening?

After searching about it, I learned that for each deployment, Firebase is preparing a container with the artifacts so it can be used a serverless function [*] WRITE MORE.
[ADD Screenshot].

## The solution

There are few steps to avoid this sudden increase in storage.

### Import GStorage into Firebase to check the usage.

### Set lifecycle for the artifacts.
