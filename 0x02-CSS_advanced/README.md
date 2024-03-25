CSS Box Alignment Module Level 3
Editor’s Draft, 2 February 2024

More details about this document
This version:
https://drafts.csswg.org/css-align/
Latest published version:
https://www.w3.org/TR/css-align-3/
Feedback:
CSSWG Issues Repository
Inline In Spec
Editors:
Elika J. Etemad / fantasai (Apple)
Tab Atkins Jr. (Google)
Suggest an Edit for this Spec:
GitHub Editor
Copyright © 2024 World Wide Web Consortium. W3C® liability, trademark and permissive document license rules apply.

Abstract
This module contains the features of CSS relating to the alignment of boxes within their containers in the various CSS box layout models: block layout, table layout, flex layout, and grid layout. (The alignment of text and inline-level content is defined in [CSS-TEXT-3] and [CSS-INLINE-3].)

CSS is a language for describing the rendering of structured documents (such as HTML and XML) on screen, on paper, etc.
Status of this document
This is a public copy of the editors’ draft. It is provided for discussion only and may change at any moment. Its publication here does not imply endorsement of its contents by W3C. Don’t cite this document other than as work in progress.

Please send feedback by filing issues in GitHub (preferred), including the spec code “css-align” in the title, like this: “[css-align] …summary of comment…”. All issues and comments are archived. Alternately, feedback can be sent to the (archived) public mailing list www-style@w3.org.

This document is governed by the 03 November 2023 W3C Process Document.

The following features are at-risk, and may be dropped during the CR period:

[ first | last ]? baseline
the <overflow-position> keywords
the scrollable-area safety trigger into safe mode when no <overflow-position> is specified
the legacy keyword for justify-items
the effect of the box alignment properties on absolutely-positioned boxes with auto offsets
“At-risk” is a W3C Process term-of-art, and does not necessarily imply that the feature is in danger of being dropped or delayed. It means that the WG believes the feature may have difficulty being interoperably implemented in a timely manner, and marking it as such allows the WG to drop the feature if necessary when transitioning to the Proposed Rec stage, without having to publish a new Candidate Rec without the feature first.

table of contents
1Introduction
1.1Module Interactions
1.2Value Definitions
1.3Partial Implementations
2Overview of Alignment Properties
3Alignment Terminology
4Alignment Keywords
4.1Positional Alignment: the center, start, end, self-start, self-end, flex-start, flex-end, left, and right keywords
4.2Baseline Alignment: the baseline keyword and first/last modifiers
4.3Distributed Alignment: the stretch, space-between, space-around, and space-evenly keywords
4.4Overflow Alignment: the safe and unsafe keywords and scroll safety limits
5Content Distribution: Aligning a Box’s Contents Within Itself
5.1The justify-content and align-content Properties
5.1.1Block Containers (Including Table Cells)
5.1.2Multicol Containers
5.1.3Flex Containers
5.1.4Grid Containers
5.2Content-Distribution Shorthand: the place-content property
5.3Overflow and Scroll Positions
5.4Baseline Content-Alignment
6Self-Alignment: Aligning the Box Within Its Parent
6.1Inline-Axis (or Main-Axis) Alignment: the justify-self property
6.1.1Block-Level Boxes
6.1.2Absolutely-Positioned Boxes
6.1.3Table Cells
6.1.4Flex Items
6.1.5Grid Items
6.2Block-Axis (or Cross-Axis) Alignment: the align-self property
6.2.1Block-Level Boxes
6.2.2Absolutely-Positioned Boxes
6.2.3Table Cells
6.2.4Flex Items
6.2.5Grid Items
6.3Self-Alignment Shorthand: the place-self property
6.4Baseline Self-Alignment
6.5Effects on Sizing of Absolutely Positioned Boxes with Static-Position Insets
7Default Alignment
7.1Inline-Axis (or Main-Axis) Alignment: the justify-items property
7.2Block-Axis (or Cross-Axis) Alignment: the align-items property
7.3Self-Alignment Shorthand: the place-items property
8Gaps Between Boxes
8.1Row and Column Gutters: the row-gap and column-gap properties
8.2Gap Shorthand: the gap property
8.3Percentages In gap Properties
8.4Legacy Gap Properties: the grid-row-gap, grid-column-gap, and grid-gap properties
9Baseline Alignment Details
9.1Determining the Baselines of a Box
9.2Baseline Alignment Grouping
9.3Aligning Boxes by Baseline
Appendix A: Static Position Terminology
10Changes
11Privacy Considerations
12Security Considerations
Acknowledgments
Conformance
Document conventions
Conformance classes
Partial implementations
Implementations of Unstable and Proprietary Features
Non-experimental implementations
Index
Terms defined by this specification
Terms defined by reference
References
Normative References
Informative References
Property Index
Issues Index
1. Introduction
CSS Levels 1 and 2 allowed for the alignment of text via text-align and the alignment of blocks by balancing auto margins. However, except in table cells, vertical alignment was not possible. As CSS adds further capabilities, the ability to align boxes in various dimensions becomes more critical. This module attempts to create a cohesive and common box alignment model to share among all of CSS.

NOTE: The alignment of text and inline-level content is defined in [CSS-TEXT-3] and [CSS-INLINE-3].

NOTE: This specification is not intended to change any of the behavior defined in CSS2.1 when the properties defined here are set to their initial values. If implementors or anyone else notices a discrepancy, please report this to the CSSWG as an error.

This section (above) is not normative.

1.1. Module Interactions
This module adds some new alignment capabilities to the block layout model described in [CSS2] chapters 9 and 10, redefines how overconstrained block-level box margins are resolved, and defines the interaction of these new alignment properties with the alignment of table cell content using vertical-align, as defined in [CSS2] chapter 17.

The interaction of these properties with Grid Layout [CSS-GRID-1] and Flexible Box Layout [CSS-FLEXBOX-1] is defined in their respective modules. The property definitions here supersede those in [CSS-FLEXBOX-1] (which have a smaller, earlier subset of permissible values).

No properties in this module apply to the ::first-line or ::first-letter pseudo-elements.

1.2. Value Definitions
This specification follows the CSS property definition conventions from [CSS2] using the value definition syntax from [CSS-VALUES-3]. Value types not defined in this specification are defined in CSS Values & Units [CSS-VALUES-3]. Combination with other CSS modules may expand the definitions of these value types.

In addition to the property-specific values listed in their definitions, all properties defined in this specification also accept the CSS-wide keywords as their property value. For readability they have not been repeated explicitly.

1.3. Partial Implementations
Since it is expected that support for the features in this module will be deployed in stages corresponding to the various layout models affected, it is hereby clarified that the rules for partial implementations that require treating as invalid any unsupported feature apply to any alignment keyword which is not supported across all layout modules to which it applies for layout models in which the implementation supports the property in general.

For example, if an implementation supports align-self in [CSS-GRID-1] and [CSS-FLEXBOX-1], then it must treat start as invalid unless it is supported in both grid and flex containers. However if that same implementation does not support align-self for block-level elements at all, then a lack of implementation of align-self: start does not trigger this requirement to treat it as invalid.

2. Overview of Alignment Properties
The box alignment properties in CSS are a set of 6 properties that control alignment of boxes within other boxes. They can be described along two axises:

which dimension they apply to (main/inline vs. cross/block), and
whether they control the position of the box within its parent, or the box’s content within itself.
NOTE: This specification uses the terms “justify” and “align” to distinguish between alignment in the main/inline and cross/block dimensions, respectively. The choice is somewhat arbitrary, but having the two terms allows for a consistent naming scheme that works across all of CSS’s layout models (including CSS Flexbox 1 § 2 Flex Layout Box Model and Terminology)

The following table summarizes the box alignment properties and the display types they can apply to.

Common	Axis	Aligns	Applies to
justify-content	main/inline	content within element
(effectively adjusts padding)
block containers, flex containers, and grid containers
align-content	cross/block
justify-self	inline	element within parent
(effectively adjusts margins)
block-level boxes, absolutely-positioned boxes, and grid items
align-self	cross/block	absolutely-positioned boxes, flex items, and grid items
justify-items	inline	items inside box
(controls child items’ justify-self: auto)
block containers and grid containers
align-items	cross/block	flex containers and grid containers
NOTE: The *-items properties don’t affect the element itself. When set on a container, they specify the interpretation of any *-self: auto used on children of the container element.

3. Alignment Terminology
Since this module defines alignment properties for all layout modes in CSS, some abstract terminology is introduced:

alignment subject
The alignment subject is the thing or things being aligned by the property. For justify-self and align-self, the alignment subject is the margin box of the box the property is set on, and assumes the writing mode of that box. For justify-content and align-content, the alignment subject is defined by the layout mode and refers to some aspect of its contents; it also assumes the writing mode of the box the property is set on.
alignment container
The alignment container is the rectangle that the alignment subject is aligned within. This is defined by the layout mode, but is usually the alignment subject’s containing block, and assumes the writing mode of the box establishing the containing block.
fallback alignment
Some alignments can only be fulfilled in certain situations or are limited in how much space they can consume; for example, space-between can only operate when there is more than one alignment subject, and baseline alignment, once fulfilled, might not be enough to absorb all the excess space. In these cases a fallback alignment takes effect (as defined below) to fully consume the excess space.
4. Alignment Keywords
All of the alignment properties use a common set of keyword values, which are defined in this section. Keywords fall into three categories:

positional alignment
These keywords define alignment as an absolute position within the alignment container.
baseline alignment
These keywords define alignment as a relationship among the baselines of multiple alignment subjects within an alignment context.
distributed alignment
These keywords define alignment as a distribution of space among alignment subjects.
4.1. Positional Alignment: the center, start, end, self-start, self-end, flex-start, flex-end, left, and right keywords
The positional alignment keywords specify a position for an alignment subject with respect to its alignment container.

Values have the following meanings:

center (self, content)
Centers the alignment subject within its alignment container.
start (self, content)
Aligns the alignment subject to be flush with the alignment container’s start edge in the appropriate axis.
end (self, content)
Aligns the alignment subject to be flush with the alignment container’s end edge in the appropriate axis.
self-start (self)
Aligns the alignment subject to be flush with the edge of the alignment container corresponding to the alignment subject’s start side in the appropriate axis.
self-end (self)
Aligns the alignment subject to be flush with the edge of the alignment container corresponding to the alignment subject’s end side in the appropriate axis.
flex-start (self, content)
Only used in flex layout. [CSS-FLEXBOX-1] Aligns the alignment subject to be flush with the edge of the alignment container corresponding to the flex container’s main-start or cross-start side, as appropriate.
When used outside of a flex formatting context, this value behaves as start. That is, on boxes that are not flex items (or pretending to be flex items, such as when determining the static position of an absolutely-positioned box that is a child of a flex container), this value behaves as start when used in the self-alignment properties, and on boxes that are not flex containers, this value behaves as start when used in the content-distribution properties.

flex-end (self, content)
Only used in flex layout. Aligns the alignment subject to be flush with the edge of the alignment container corresponding to the flex container’s main-end or cross-end side, as appropriate.
When used outside of a flex formatting context, this value behaves as end. That is, on boxes that are not flex items (or pretending to be flex items, such as when determining the static position of an absolutely-positioned box that is a child of a flex container), this value behaves as end when used in the self-alignment properties, and on boxes that are not flex containers, this value behaves as end when used in the content-distribution properties.

left (only justify-*)
Aligns the alignment subject to be flush with the alignment container’s line-left or physical left edge, whichever is in the appropriate axis.
If the property’s axis is not parallel with either left↔right axis, this value behaves as start. Currently, the only case where the property’s axis is not parallel with either left↔right axis is in a column flexbox.

right (only justify-*)
Aligns the alignment subject to be flush with the alignment container’s line-right or physical right edge, whichever is in the appropriate axis.
If the property’s axis is not parallel with either left↔right axis, this value behaves as start. Currently, the only case where the property’s axis is not parallel with either left↔right axis is in a column flexbox.

Two grammar terms are used to denote certain subsets of these values:

<self-position>
This set is used by justify-self and align-self to align the box within its alignment container, and also by justify-items and align-items (to specify default values for justify-self and align-self).
<self-position> = center | start | end | self-start | self-end |
        flex-start | flex-end
<content-position>
This set is used by justify-content and align-content to align the box’s contents within itself.
<content-position> = center | start | end | flex-start | flex-end
NOTE: left and right are excluded from <self-position> and <content-position>, despite being valid positional alignment values for justify-content/justify-self/justify-items, because they are not allowed in the align-* properties. They are instead explicitly included in the justify-* properties’ grammars.

The start and end keywords are flow-relative: they use the writing mode to determine which side to align to.
Inline-axis 'start' alignment:
			     Horizontal Latin and Chinese are left-aligned,
			     while Arabic and Hebrew are right-aligned. Inline-axis 'end' alignment:
			     Horizontal Latin and Chinese are right-aligned,
			     while Arabic and Hebrew are left-aligned.
start vs end in the inline axis (typically† justify-*)
The left and right keywords are absolute (not flow-relative).

Inline-axis 'left' alignment:
			     Horizontal text is left-aligned, regardless of writing system. Inline-axis 'right' alignment:
			     Horizontal text is right-aligned, regardless of writing system.
left vs right
The start and end keywords have meaning in both the inline and block axes: start always orients to the start of the text (top left for left-to-right/top-to-bottom languages like English) while end always orients to the end of the text.

Block-axis 'start' alignment:
			     Horizontal text is top-aligned in the vertical axis. Block-axis 'bottom' alignment:
			     Horizontal text is bottom-aligned in the vertical axis.
start vs end in the block axis (typically† align-*)
The start and end keywords use the writing mode of the alignment container, to help keep things consistent. But if alignment using the alignment subject’s writing mode is needed, the self-start and self-end keywords can be used.

Inline-axis 'start' alignment in an LTR container:
			     Alignment uses the context’s start direction, so
			     the (RTL) Arabic and Hebrew items
			     are left-aligned alongside the (LTR) Latin and Chinese. Inline-axis 'self-start' alignment in an LTR container:
			     Horizontal Latin and Chinese items are right-aligned,
			     while Arabic and Hebrew items are left-aligned.
start vs self-start on the individual items
The behavior of the alignment keywords is analogous in vertical writing modes: start and end are relative to the start/end of the text in the relevant axis. The left and right keywords are interpreted as line-left and line-right, relative to the “left” and “right” sides of LTR/RTL text.
Inline-axis 'start' alignment in vertical-rl writing:
			     Vertical Latin and Chinese are top-aligned,
			     while Arabic and Hebrew are bottom-aligned. Inline-axis 'end' alignment in vertical-rl writing:
			     Vertical Latin and Chinese are top-aligned,
			     while Arabic and Hebrew are bottom-aligned.
start vs end in the inline axis (typically† justify-*)
Inline-axis 'left' alignment in vertical-rl writing:
			     Vertical text is top-aligned, regardless of writing system. Inline-axis 'right' alignment in vertical-rl writing:
			     Vertical text is bottom-aligned, regardless of writing system.
left vs right
Block-axis 'start' alignment in vertical-rl writing:
			     Vertical text is top-aligned in the vertical axis. Block-axis 'bottom' alignment in vertical-rl writing:
			     Vertical text is bottom-aligned in the vertical axis.
start vs end in the block axis (typically† align-*)
Inline-axis 'start' alignment in a vertical-rl LTR container:
			     Alignment uses the context’s start direction, so
			     the (RTL) Arabic and Hebrew items
			     are top-aligned alongside the (LTR) Latin and Chinese. Inline-axis 'self-start' alignment in a vertical-rl LTR container:
			     Horizontal Latin and Chinese items are top-aligned,
			     while Arabic and Hebrew items are bottom-aligned.
start vs self-start on the individual items
For most layout models (block, table, grid, etc), the justify-* properties always align things in the inline axis, while the align-* properties always align things in the block axis.
Flexbox, on the other hand, has justify-* align things in the main axis and align-* align things in the cross axis. This depends on the value of flex-direction: when flex-direction is row or row-reverse, it matches the other layout modes (inline axis with justify-*, block axis with align-*); when flex-direction is column or column-reverse, it has the opposite correspondence.

 Make it easier to understand the dual-axis nature of "start" and "end" wrt orthogonal flows.

4.2. Baseline Alignment: the baseline keyword and first/last modifiers
See CSS Writing Modes 3 § 4.1 Introduction to Baselines.

Baseline alignment is a form of positional alignment that aligns multiple alignment subjects within a shared alignment context (such as cells within a row) by matching up their alignment baselines. If the position of the alignment subjects within a baseline-sharing group is not fully constrained by baseline alignment (i.e., they could be shifted within their respective alignment containers while maintaining baseline-alignment), they are fallback-aligned insofar as possible while preserving their baseline alignment.`
