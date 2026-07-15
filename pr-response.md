# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- fill in at the end -->

## Comment 1 — Rename
**What I did:** renamed the function save_to_watchlist() to add_to_watchlist
**How I verified:** checked for any save_to_watchlist left unedited. changed them to add_to_watchlist. Confirmed tests worked

## Comment 2 — Deduplication
**What I did:** Added the Already in watchlist error exception. added the dedup check to add_to_watchlist()
**How I verified:** ran pytest tests/ -v, all were passing

## Comment 3 — Missing test
**What I did:** created tests/test_watchlist.py followed the same fixture as the collection.py
**How I verified:** I confirmed that all three tests passed. 

## Comment 4 — Default visibility
**My position:** Change the default to False
**Reasoning:** Watch lists show a person's intent or interests. Because watchlists can contain more personal information of the user to other users, I recommend keeping the default at false. This way the user has a choice to make it public and its intentional they want this information public. 
**Tradeoff acknowledged:** This could limit the social value. This could mean many watchlists are on private, which coupd supress the value of the product. 

## Comment 5 — Sort order
**My position:** switched watchlist sort order from alphabetical to date order. 
**Reasoning:** Most users would want to see what was recently added without having to scroll. This would match with get collection which already sorts by date. 
**Engagement with reviewer's point:** I agree, the user would want to see what was recently added. In a watchlist, it is popular for the list to be in date order. I implemented the suggestion

## Comment 6 — Rebase
**What conflicted:** models.py conflicted because the watchlist entry needed to be updated form db.Integer to db.String(36)
**How I resolved it:** Updated `WatchlistEntry.film_id` to `db.String(36)` with the same `db.ForeignKey("film.id")` reference as `CollectionEntry`, keeping the rest of the model unchanged. Also added a `UniqueConstraint` on `(user_id, film_id)` to match the collection model's pattern.
**How I verified no conflict remains:** Ran `pytest tests/ -v` — all 7 tests passed. Also searched the codebase for any remaining integer-typed `film_id` references 

## PR Description
<!-- write at the end -->