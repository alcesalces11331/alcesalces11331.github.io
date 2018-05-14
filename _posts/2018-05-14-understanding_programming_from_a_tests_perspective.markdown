---
layout: post
title:      "Understanding Programming From A Test's Perspective"
date:       2018-05-14 22:37:22 +0000
permalink:  understanding_programming_from_a_tests_perspective
---


Perhaps, from day one, the first lesson we learned -- and from which all other lessons are abstractions of -- was the logical implications. The first word spoken was Boolean, which roughly translates as: that which can only be either/or; that which can only be true or it can be false. "Ok," all the students uttered in unison, Boolean. A simple concept and one already incorporated into everyday existence, perhaps, in itself, from day one. It is cause and effect glorified. Truth. Without delving deeper into *shades* of truth, i.e., Kleene logic, i.e., *fuzzy* logic, it can be only be *a* or *b*.

This next section is akin to a fall from glory, the proverbial fall from grace, as the single most important tenet had been forgotten. It was thrown to the wind and errors started popping up in line after line. The mastery of arrays and hashes fizzled when their return values were forsaken. "I... uhh... mean, what exactly is the return value and why is it important?

```
array = [:arbitrary_answer, :truthiness, :utter_confusion]
array.each do |truth|
    puts truth.to_s << '?'
end
```

When followed, return values are the bread crumbs and errors are like the evil, vile witch which wants only to be loved. The return values appear like trivialities at first, simply because they're not extensively being reused and incorporated until much later on in the lessons. However, it is the lessons which should never be forgotten and first to exit from error clogged minds. This is importantly true when the specs written to test the students *evolve* into passing ids and symbols through Capybara instead of ol' reliable, rspec. Not to mention the tests having to systematically scrape the code with Nokogiri. All passing elements to functions and **spitting out return values** -- which, if anyone has been paying attention register **TRUE OR FALSE**. Trust this coder, listening to the sweet sublime tones of return values and paying attention to these often overlooked features pays dividends in the future.
