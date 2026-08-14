# recipes

A "Hello world!" program that is also a cake recipe.

[Chef](https://www.dangermouse.net/esoteric/chef.html) is an esoteric
programming language by David Morgan-Mar with one delightful design goal:
a program should read as a genuine recipe. Not *look* like one — read like
one, ingredients and method, the sort of thing you could plausibly find on
a recipe card.

`cake_with_chocolate_sauce.chef` is that, and it prints `Hello world!`.

## How it works

Chef's data structures are kitchen equipment. The **mixing bowl** is a stack.
The **baking dish** is the output buffer. Ingredients are variables, and an
ingredient's quantity is its value.

The trick to reading a Chef program is that those quantities are ASCII codes.
Once you know that, the ingredient list stops being a recipe and starts being
a string, hidden in plain sight:

| Ingredient | Amount | ASCII |
| --- | --- | --- |
| milk chocolate | 72 g | `H` |
| dark chocolate | 101 g | `e` |
| hot water | 108 ml | `l` |
| heated double cream | 108 ml | `l` |
| sugar | 111 g | `o` |

That's the chocolate sauce: `Hello`. The cake carries the rest — 32 g of cocoa
powder is a space, 119 ml of flour is `w`, 100 g of butter is `d`, 33 g of
chocolate chips is `!`.

The method section then does the actual computation. `Put ... into the mixing
bowl` pushes onto the stack. `Stir the mixing bowl for n minutes` buries the
top ingredient n levels down, which is how the letters get into the right
order. `Liquefy` converts numbers to characters, and `Pour contents of the
mixing bowl into the baking dish` sends them to output — in reverse, because
it's a stack.

A few lines are pure garnish. `Bake the cake mixture` / `Wait until baked` is
a loop over an ingredient declared as `0 g`, so the body never runs. The oven
temperature and cooking time are ignored entirely. They're there because the
recipe would look wrong without them, which is the whole point of the language.

## Running it

There's no toolchain to install — paste the file into an online interpreter:

**https://esolangpark.vercel.app/ide/chef**

Expected output:

```
Hello world!
```

## Can you actually bake it?

The proportions are not insane — 114 g sugar, 119 g flour, 100 g butter, 111 ml
egg, 32 g cocoa, 2 pinches baking powder is a recognisable chocolate cake, and
the sauce is a standard ganache. Whether it's *good* is untested. The constraint
runs the other way in Chef: the numbers are fixed by the text you want to print,
and the recipe has to be talked into making sense around them.
