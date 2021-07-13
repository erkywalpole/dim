# A System for Choosing Which Armor to Keep in Destiny 2

Before I get started, this is all about armor pieces. Weapons aren’t included in these filters.

In the past, I have had trouble figuring out which armor drops to keep, and which to dismantle. I mostly looked for spikes in recovery and intellect since these are expensive to mod up. That was about as deep as I went. All the while I knew that, overall, I was making arbitrary decisions and making them inconsistently. My vault ballooned as a result. 

This is why I was so excited to a [post](https://reddit.com/r/DestinyItemManager/comments/kujvqt/i_made_a_filter_for_destiny_item_manager_to_clean/) detailing how one person uses filters to help them make decisions about which armor to dismantle. As I played around with it, I found the filter itself was too broad for my taste. It ended up highlighting very few pieces for dismantling. So, I took a closer look through the filter, and it inspired me to make my own.

Instead of one giant overly inclusive filter that covers all reasons to keep an armor piece, I decided to take a tiered approach to keeping armor. You can use the tiers based on how picky you are about your armor. The more you play (or the longer you’ve played), the picker you’ll want to be. 

## Tier 1

For example, when you’re first getting started with Destiny or coming back after a long absence, what’s most important is just finding decent, even rolls at any rarity that add at least 10 points to each stat. Here’s a filter that would help you find those pieces, which I'm calling **Tier 1**:

`is:armor not:classitem -tag:keep -tag:archive -tag:favorite -tag:infuse not:inloadout not:masterwork -(basestat:mobility:>=8 basestat:resilience:>=8 basestat:recovery:>=8 basestat:discipline:>=8 basestat:intellect:>=8 basestat:strength:>=8)`

You can paste it into DIM and see what it does. I basically pulled it straight from the previous filter. A reminder: the way these filters work is they highlight things that *don’t* match the criteria you set so you know what you can safely tag as junk and dismantle.

## Tier 2

After playing D2 for a while, you start getting pickier. The idea here is you want armor pieces that are going to contribute 15-20 points to your stats, and you may be getting pickier about which stats those are. This is **Tier 2**:

`is:armor -tag:keep -tag:archive -tag:favorite -tag:infuse not:inloadout not:masterwork
(
(
not:classitem
-(
(is:hunter ((basestat:recovery:>=13 basestat:mobility:>=13) or (basestat:recovery:>=13 basestat:intellect:>=13) or (basestat:intellect:>=13 basestat:mobility:>=13) or basestat:mobility:>=18)) or 
(is:titan ((basestat:resilience:>=13 basestat:strength:>=13) or (basestat:recovery:>=13 basestat:strength:>=13) or (basestat:recovery:>=13 basestat:resilience:>=13) or basestat:resilience:>=18)) or 
(is:warlock ((basestat:recovery:>=13 basestat:discipline:>=13) or (basestat:recovery:>=13 basestat:intellect:>=13) or (basestat:intellect:>=13 basestat:discipline:>=13) or basestat:intellect:>=18 or basestat:recovery:>=18)) or 
basestat:total:>=62 or 
basestat:custom:>=39
)
) or
is:blue
)`

The great thing about this approach (and the upcoming Tier 3 filter) is it’s effectively a framework. If you don’t prefer these stats for your Titan or any character, you can absolutely change them to meet your play style. 

## Tier 3

And finally, there’s **Tier 3**. You’ve been playing for a long while. You have some great armor sets. You only want to replace them with even more amazing pieces. This tier is for your god rolled armor pieces and for armor pieces that will contribute 25+ points to certain stats, giving you a chance at 100 without any mods.

`is:armor -is:maxpower -tag:keep -tag:archive -tag:favorite -tag:infuse not:inloadout not:masterwork
(
(
not:classitem
-(
(is:hunter ((basestat:mobility:>=18 basestat:recovery:>=23) or (basestat:mobility:>=23 basestat:total:>=62))) or 
(is:titan (basestat:recovery:>=23 or (basestat:resilience:>=18 basestat:strength:>=13 basestat:discipline:>=13) or (basestat:strength:>=23  basestat:total:>=62))) or 
(is:warlock (basestat:recovery:>=28 or (basestat:recovery:>=23 basestat:discipline:>=18) or (basestat:intellect:>=23 basestat:total:>=62))) or 
(not:hunter basestat:mobility:>=23 basestat:custom:>=24) or 
(not:warlock basestat:discipline:>=23 basestat:custom:>=24) or 
(not:titan basestat:strength:>=23 basestat:custom:>=24) or
(not:titan basestat:resilience:>=10 basestat:custom:>=39) or 
basestat:total:>=67 or 
basestat:custom:>=48
)
) or
is:blue
)`

Couple of notes:

* As mentioned above, this filter highlights the armor that is safe to dismantle. The reason it works that way is so you can use the bulk tag feature to mark the armor as junk.
* This doesn’t currently take power leveling into account. During that stage of play, people should add a `not:maxpower` to the first line.
* All stat filters assume you'll masterwork the piece. E.g., we are filtering for 18+ stat armor because when masterworked, it will go up to 20+.
* Filters are helped by, but not dependent upon, people using the custom stats feature in DIM, and assume that people are choosing three stats per character class. The [DIM wiki](https://destinyitemmanager.fandom.com/wiki/Organizer#Custom_Stat_Total_.28Custom_Total.29) has more info.
* Class items are always excluded. You’ll have to manage those separately.
* I include exotics in these filters. I want to know if my exotics are awesome rolls, too. Most of them aren’t, and so I tag them `keep` and that excludes them from the filter. You could also add `not:exotic` to the first line to *always* exclude exotics from the filter.

**TL;DR**

How stringent do you want to be about which armor you keep? Not at all, somewhat, or extremely stringent? Use the filter that corresponds to how stringent you are with your armor drops:

* Not at all = Tier 1
* Somewhat = Tier 2
* Extremely = Tier 3

Dismantle whatever is highlighted by the filter or tag it as `keep` to exclude it.