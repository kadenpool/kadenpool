# Kaden Pool: Vesuvius Challenge work, Aug to Sep 2026

I work with the published scroll data and fix what gets in the way of reading it: a tool that lines up
two scans of the same scroll, fixes to the challenge's own code, problems found in its catalogue and
transforms, and two write-ups that ship with their data.

## Used by others

- [#1665](https://github.com/ScrollPrize/villa/pull/1665) and [#1731](https://github.com/ScrollPrize/villa/pull/1731) are merged into villa.
- Bullo27 reproduced [#1665](https://github.com/ScrollPrize/villa/pull/1665) and [#1676](https://github.com/ScrollPrize/villa/pull/1676) independently, on Linux.
- SurgeFok's [vesuvius-catalog-check](https://github.com/SurgeFok/vesuvius-catalog-check) checks its own detector against [#1730](https://github.com/ScrollPrize/villa/issues/1730): it finds 20, #1730 reports 20.
- hendrikschilling reviewed [#1676](https://github.com/ScrollPrize/villa/pull/1676) and [#1682](https://github.com/ScrollPrize/villa/pull/1682) on 21 Sep; both now carry the changes he asked for.

## The tool

- [scroll-lineup](https://github.com/kadenpool/scroll-lineup): two public OME-Zarr scans of one scroll in, a transform in the challenge's own format out. Graded against every published transform: 13 PASS, 9 WEAK and 4 FAIL over all 26 official pairs, nothing excluded.

## Fixes to the challenge's code: silent wrong answers made loud

- [#1731](https://github.com/ScrollPrize/villa/pull/1731) (merged): surfaces whose stored bbox carries the `-1` marker were returned for heights they never touch.
- [#1665](https://github.com/ScrollPrize/villa/pull/1665) (merged): reading the public bucket no longer needs AWS credentials, or reports that the data does not exist.
- [#1847](https://github.com/ScrollPrize/villa/pull/1847): a failed remote chunk fetch ends `vc_grow_seg_from_seed` with one line and exit 1, not an abort. Report: [#1846](https://github.com/ScrollPrize/villa/issues/1846).
- [#1676](https://github.com/ScrollPrize/villa/pull/1676): a region past the edge of a dataset is refused instead of written past the buffer, and every caller now checks.
- [#1682](https://github.com/ScrollPrize/villa/pull/1682): `create_level_dataset` works under zarr 3, and `overwrite=False` no longer empties a level.
- [#1717](https://github.com/ScrollPrize/villa/pull/1717) (draft): a render partly outside its volume says how much: 47.1 % on a published surface.
- [#1766](https://github.com/ScrollPrize/villa/pull/1766) (draft) and [#1765](https://github.com/ScrollPrize/villa/issues/1765): the 2 um ink model's README window, centred on the surface, reproduces the published ink maps.
- [#1769](https://github.com/ScrollPrize/villa/pull/1769) (draft): VC3D stops seeding a bounding box from the `-1` missing-point marker.
- [#1664](https://github.com/ScrollPrize/villa/pull/1664) (closed to stay under villa's open-PR limit; the problem is unchanged): a failed ink-label download is reported instead of a blank image.

## Found in the catalogue and transforms

- [#1835](https://github.com/ScrollPrize/villa/issues/1835): four published volume transforms do not fit their own published landmarks.
- [#1843](https://github.com/ScrollPrize/villa/issues/1843): PHerc1667's 1.129 um to 2.399 um transform misses its landmarks by 123 um; a fit to the same landmarks misses by 2.2 um.
- [#1845](https://github.com/ScrollPrize/villa/issues/1845): rendering a segment from its coarser published mesh costs 0.04 AUC.
- [#1730](https://github.com/ScrollPrize/villa/issues/1730): 20 published segments name a source volume scanned after the segment was made.
- [#1734](https://github.com/ScrollPrize/villa/issues/1734): for 28 PHercParis4 segments, the catalogue's bounding box is computed from the `-1` marker.

## Reports, each with its data and a script that re-derives its numbers

- [Ink negative controls](https://github.com/kadenpool/scroll-lineup/tree/main/reports/ink-negative-controls): four controls that tell a real ink reading from papyrus texture, on PHerc0846A, PHerc0813 and PHerc0211.
- [A First Letters attempt on PHerc1203](https://github.com/kadenpool/scroll-lineup/tree/main/reports/pherc1203-first-letters): two scans, no published transform between them, and what it took to read across.

## Helping with others' work

- [#1809](https://github.com/ScrollPrize/villa/issues/1809): comments on Bullo27's crash report; his fix, [#1817](https://github.com/ScrollPrize/villa/pull/1817), uses my test server and my macOS run in its proof table.
- [#1818](https://github.com/ScrollPrize/villa/pull/1818#issuecomment-5748183068): a reading test on spelufo's bicubic-interpolation branch, to put a number beside its pictures.
- Independent checks of others' results: [corpus-ink-survey #1](https://github.com/TAUIL-Abd-Elilah/corpus-ink-survey/issues/1) and [ink9um-z-window-selection #1](https://github.com/tarikcankorkmaz00/ink9um-z-window-selection/issues/1).

## Outside villa

- [ScrollFiesta #16](https://github.com/Hob3rMallow/scrollfiesta_public/pull/16): a published atlas mesh keeps its texture coordinates when converted for villa's tools.

---

Built with Claude Code under my direction. I found most of these problems myself while working with the
published data, and checked the evidence for each.
