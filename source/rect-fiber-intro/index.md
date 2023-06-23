---
title: react fiber 簡介
date: 2021-10-26 01:02:22
---

一般來說，我們在 react 針對畫面開發的動作僅限在 `component` ，

用 `jsx` 描述完 `react element` 後，渲染到實際畫面的動作就由 react 本身來進行，

`react element` 轉譯成 `virtual dom` 後， 在針對舊有的 `virtual dom` 對比(假如有)，最後準備上到`真實畫面`

這過程叫做 `reconciliation`，

而執行 `reconciliation` 的叫做 `reconciler`，

`reconciler` 分兩種：

## stack reconciler

這是使用在 `react 15` 或是更早的版本，


## fiber reconciler
