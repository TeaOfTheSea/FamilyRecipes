---
title: "My Family Recipes"
description: 'A Collection of Recipes from Multiple of my Family Members.'
layout: single
---

## Cookbooks:

{{< tagcloud >}}

## About:

This site is a fork of [based.cooking](https://based.cooking/) that I made because the original site prohibits sweets. Instead of just being a baking recipe site however, I've decided to go the direction of trying to archive a few family cookbooks in their entirety to preserve my family's culinary tradition somewhat.

## Open source and accepting contributions, but not for recipes.

In the spirit of the website whose code I am using, the entirety of this site can be found [on Github](https://github.com/TeaOfTheSea/FamilyRecipes).
That said, this is a personal project to preserve the recipes of my family, so I won't be accepting recipe submissions. If you do want to contribute for some reason, however, feel free to submit a picture of anything you bake, or fill in any of the missing information related to prep times and serving sizes.

## Search All Recipes:

<div class="search js-only">
  <input type="text" id="search" placeholder="Search ALL Recipes...">
  <button id="clear-search">
    <svg xmlns="http://www.w3.org/2000/svg" class="ionicon" viewBox="0 0 512 512"><title>Backspace</title><path d="M135.19 390.14a28.79 28.79 0 0021.68 9.86h246.26A29 29 0 00432 371.13V140.87A29 29 0 00403.13 112H156.87a28.84 28.84 0 00-21.67 9.84v0L46.33 256l88.86 134.11z" fill="none" stroke="currentColor" stroke-linejoin="round" stroke-width="32"></path><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="32" d="M336.67 192.33L206.66 322.34M336.67 322.34L206.66 192.33M336.67 192.33L206.66 322.34M336.67 322.34L206.66 192.33"></path></svg>
  </button>
</div>

<script>
// @license magnet:?xt=urn:btih:5ac446d35272cc2e4e85e4325b146d0b7ca8f50c&dn=unlicense.txt Unlicense

document.addEventListener("DOMContentLoaded", () => {
  for (e of document.getElementsByClassName("js-only")) {
    e.classList.remove("js-only");
  }

  const recipes = document.querySelectorAll("#artlist li");
  const search = document.getElementById("search");
  const clearSearch = document.getElementById("clear-search");
  const artlist = document.getElementById("artlist");

  search.addEventListener("input", () => {
    // grab search input value
    const searchText = search.value.toLowerCase().trim().normalize('NFD').replace(/\p{Diacritic}/gu, "");
    const searchTerms = searchText.split(" ");
    const hasFilter = searchText.length > 0;

    artlist.classList.toggle("list-searched", hasFilter);

    // for each recipe hide all but matched
    recipes.forEach(recipe => {
      const searchString = `${recipe.textContent} ${recipe.dataset.tags}`.toLowerCase().normalize('NFD').replace(/\p{Diacritic}/gu, "");
      const isMatch = searchTerms.every(term => searchString.includes(term));

      recipe.hidden = !isMatch;
      recipe.classList.toggle("matched-recipe", hasFilter && isMatch);
    })
  })

  clearSearch.addEventListener("click", () => {
    search.value = "";
    recipes.forEach(recipe => {
      recipe.hidden = false;
      recipe.classList.remove("matched-recipe");
    })

    artlist.classList.remove("list-searched");
  })
})
// @license-end
</script>

{{< artlist >}}

