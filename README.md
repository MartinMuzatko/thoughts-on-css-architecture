# Thoughts on CSS Architecture

Here you can find my ordered or unordered elaborate thoughts about CSS architectures and systems.
What my personal reasoning is for and against various systems.

## My personal journey

I have been working on many small and large-scale web-apps, sites, and components. In almost 12 years of experience with CSS and all the old and new specifications, at the beginning of every project I am yet again faced with the different design choices to make. Knowing SMACSS, OOCSS and even BEM (and having used those), it is still tough to decide for one way to organize the project at hand.

Of course, different approaches speak to different kinds of peoples with their own needs and worldviews on how something should be made or maintained or built with.

## Tools and Abstractions

Whenever a new framework or library comes around, I am astonished of all the opportunities discovered by combining different styles and laying them out in a clever way with whatever naming convention is trendy at the moment. To ease development.

When I first discovered attribute selectors in conjunction with flexbox ([flexproperties](https://www.npmjs.com/package/flexproperties)), I was obsessed how a few HTML attributes can ease working with layouts and hide the CSS required for it.

But in the end, it is just smart re-use of what already is there: The CSS specification at its core. CSS Properties and rules.

However, **this is your job** as front-end developer. Creating new tools and using existing ones and combining those.

## Frameworks

I rarely use monolithic frameworks like foundation, bootstrap, material or ui-kit. At least not all of it. The theming and layout needs of projects differ so much, that rarely one tool solves all the problems. Most of the time you end up overwriting most of the styles. This leads to the effect that you have more filesize than required. I need to be able to pick only the components that I require and configure them the way I need them.

## Code output

Mixins/Extend

## Components

### Requirements for components

#### Section




## De/Coupling

Previously, in the pre-processor of my choice:

```less
.card {
    h2,h3,h4 {
        margin-top: 0; //reset base margin
    }
}
```

The underlying HTML

```html
<div class="card">
    <h3>Title of that card</h3>
    Some content
</div>
```

I know - tight coupling to bind heading styling to the direct elements.

And while you think: yes! of course h2,h3 and h4. what else would someone use here? We assume nobody is going to (ab)use that component in any other way, or parts of it.

CSS Rules are **assumptions**.

If I want to re-use parts of that card component or want to abuse it, because the designer in the team came up with another idea. All of a sudden, there needs to be a little widget above the heading.

It is not only about collaborative development. I see how often I am standing in my own way. And I try to circumvent that, by adding even more logic. "Ok fine!" I say.

```less
.card {
    h2,h3,h4 {
        &:first-child {
            margin-top: 0; //reset base margin
        }
    }
}
```


We could require more markup
```less
.card {
    header {
        h2,h3,h4 {
            margin-top: 0; //reset base margin
        }
    }
}
```

We could require `.card` in order to apply styling to `.title`. But what if we have another class called title? That would interfere with the title in card.
```less
.card {
    .title {
        margin-top: 0; //reset base margin
    }
}
```

The only way here now is to provide
```less
.card {
    &__title {
        margin-top: 0; //reset base margin
    }
}
```
