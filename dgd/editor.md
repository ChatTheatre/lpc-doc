---
title: Editor Reference
layout: default
---

(Note: [quick reference](./ed-quickref.html))

<pre>
   The editor is line oriented.  It has two different modes, Command Mode and
Insert Mode.  In Command Mode, commands may be given that affect a range of
lines in the main buffer.  In Insert Mode, new lines may be added to the main
buffer.  Apart from the main buffer, lines may be copied to and from 26
secondary buffers.

   The editor remembers the current line and at most 26 marked lines in the
main buffer, and has some status-affecting variables which can be changed by the
user.


   1. Insert Mode

   In Insert Mode, each line typed by the user is inserted into the main buffer.
Insert Mode is indicated by the prompt '*'.  Insert Mode is entered with the
commands 'append', 'change' and 'insert' from Command Mode, and is left by
typing a line consisting of a single '.'.


   2. Command Mode

   In Command Mode, the user may issue commands that affect the current line,
all lines or a specified range of lines.  Command Mode is indicated by the
prompt ':'.  After a command has been executed, the new current line will
usually be displayed.  The most general format of commands is as follows:

   address1 , address2 command ! parameters count flags

   &lt;address1&gt; and &lt;address2&gt; specify the first and last line of a range of lines
that are to be affected by the command.  If no second line address is given,
the range is assumed to be &lt;address1, address1&gt;.  If no line range is specified
at all, a default range is assumed, usually just the current line.
   &lt;command&gt; is a string of letters or non-digits.
   &lt;!&gt; may be given with some commands to specify a different, but similar
operation.
   Some commands require &lt;parameters&gt;.
   A &lt;count&gt; may be given with many commands to specify the number of lines
that is to be affected by the command, as an alternative to specifying the
first and last line.  A &lt;count&gt; will always override &lt;address2&gt;, if given.
   Finally, &lt;flags&gt; may be given to affect the way in which the new current
line is displayed after the command has been executed.

   All parts are optional, even the command itself may be omitted.  A range of
lines without a following command will print the lines specified.  A single
&lt;address&gt; will set the current line to &lt;address&gt;, and the 'empty command' will
set the current line to the next line.


   2.1 Line addressing

   An &lt;address&gt; specifies a line in the main buffer.  It may be a number, '.'
or '$', a regular expression, a marked line, or an expression containing one of
the previous and an offset.  The most general format is:

   [number | . | $ | /pattern/ | ?pattern? | 'm]  [+ | -]  [number]

   Lines in the main buffer are numbered starting with 1.  A number may be
given to specify a line.  '.' denotes the current line, and '$' the last line
in the main buffer.
   A regular expression must be enclosed within '/' or '?' pairs.  '/pattern/'
will search forward, starting with the line after the current line, and
'?pattern?' will search backward.  If no pattern is specified, '//' or '??' will
respectively search forward and backward, using the previous regular expression.
If the regular expression forms the whole command, the closing '/' or '?' may be
omitted.
   A marked line is specified by a single quote "'", followed by a lowercase
letter.  The mark must have been set by the 'mark' command.

   Offsets may be given to a given &lt;address&gt; using '+' and '-', followed by
a number.  If the '+' or '-' sign is not preceded by an &lt;address&gt;, the current
line is assumed.  If the '+' or '-' sign is not followed by a number, the number
1 is assumed.  Offsets may be repeated, with a cumulative effect.

   A range of lines is indicated by &lt;address1, address2&gt;.  Either of the
addresses may be omitted:

   &lt;address, &gt;	means &lt;address, address&gt;
   &lt;, address&gt;	means &lt;., address&gt;
   &lt;,&gt;		means &lt;., .&gt;

   Alternatively, ',' can be replaced with ';'.  This has the effect of setting
the current line to &lt;address1&gt;, just before &lt;address2&gt; is evaluated.
   '%' is an alias for '1,$'.


   2.1.1 Regular expressions

   In a regular expression, characters may form a string that is searched for in
the main buffer.  Only strings on a single line can be searched for.  Some
characters and character sequences have a special meaning in regular
expressions:

   ^		matches the beginning of the line.
   $		matches the end of the line.
   .		matches any single character.
   \&lt;		matches the beginning of a word (LPC identifier).
   \&gt;		matches the end of a word (LPC identifier).
   [string]	matches any single character in the string between the square
		brackets.  a-z specifies a range of characters, and if the
		first character following the opening '[' is '^', any character
		NOT in the string is matched.
   *		matches 0, 1 or more occurances of the preceding (single
		character matching) pattern.
   \( and \)	does not match a pattern, but indicate the beginning and end of
		a subpattern that can be used in the 'substitute' command.

   If any of the symbols '^', '$', '.', '[', '*' or '\' itself is desired in
regular expressions, it should be prefixed by '\'.
   Depending on the value of the 'ignorecase' variable, which can be changed
with the 'set' command, lowercase letters may match either just the lowercase
letter or both uppercase and lowercase.  By default, only lowercase letters are
matched.


   2.1.2 Marked lines

   Lines in the main buffer can be given a mark, consisting of a lowercase
letter, which afterwards can be used in line addresses to refer to the marked
line.  This is done with the 'mark' command.


   2.2 Secondary buffers

   Apart from the main buffer, the editor maintains 26 secondary buffers which
are addressed by letters.  A range of lines from the main buffer may be copied
into a secondary buffer, and the contents of a secondary buffer may be copied
into the main buffer.  When copying lines to a secondary buffer, a lowercase
letter indicates that the previous contents of the secondary buffer (if any) is
to be replaced, and an uppercase letter indicates that the lines are to be
appended to the secondary buffer.  When copying back lines from a secondary
buffer, case of the letter specifying the buffer is not significant.


   2.2.1 Default buffer

   Each command that has the option of copying lines into a secondary buffer,
always stores the lines in a default buffer also.  If no secondary buffer is
specified when lines are copied back to the main buffer, lines are copied from
the default buffer.


   2.3 Flags

   Many commands may followed by one of the characters 'p', 'l', '#', '+' and
'-', which affect the way in which the current line is displayed after the
command is executed or, if the command itself prints lines, in which way these
lines are printed.  The characters have the following meaning:

   p	print the current line after the command has finished.  This usually
	happens automatically.
   l	print the current line after the command has finished, in 'list' format.
   #	print the current line after the command has finished, in 'number'
	format.
   +	increase the current line number by 1 before printing it.
   -	decrease the current line number by 1 before printing it.

   Flags may be repeated, with a cumulative effect.


   2.4 Multiple commands inside a global command

   More than one command may be given inside a global command, by separating
the individual commands with '|'.


   2.5 Command summary

   In the following list of commands, the default line range is shown in
parenthesis, and an optional parameter is marked with '[' ']'.  After each
command, the current line is set at the last line changed or displayed.


RANGE	COMMAND								ABBREV

(.)	append								a
	Enter Insert Mode and append lines after the specified line.
	A line address of 0 may be given to indicate that lines are to
	be inserted before the first line in the main buffer.

(.,.)	change [count]							c
	Enter Insert Mode and replace the specified lines.

(.,.)	copy address [count] [flags]					co
	Place a copy of the specified lines after the given address.
	The address may be 0, in which case the copied lines are
	inserted before the first line in the main buffer.

(.,.)	delete [buffer] [count] [flags]					d
	Delete the specified lines.  The deleted lines are saved in the
	default buffer, and in the secondary buffer if one is specified.

	edit [file]							e
	Start editing a new file.  The current main buffer and all
	secondary buffers will be discarded.  The current line will be
	placed at the last line of the main buffer.

	edit! [file]							e!
	Start editing a new file, even if the current main buffer was
	modified.

	file [file]							f
	Show statistics on the current file edited.  If an argument is
	given, the current file name is changed into the one specified.

(1,$)	global /pattern/ [command]					g
	Execute the command on all lines matching the given pattern.
	By default, the matching lines are just printed.

(1,$)	global! /pattern/ [command]					g!
	Execute the command on all lines not matching the given pattern.
	By default, the lines that don't match are just printed.

(.)	insert								i
	Enter Insert Mode and insert lines before the specified one.

(.,.+1)	join [count] [flags]						j
	Join the specified lines together in a single line.  White
	space at the beginning of a next line will be discarded.
	Unless the next line starts with ')', a space is inserted
	between two joined lines, or two spaces if the first line ends
	in '.'.

(.,.+1)	join! [count] [flags]						j!
	Join the specified lined together in a single line without
	white space processing.

(.,.)	list [count] [flags]						l
	Show the specified lines, displaying tabs as '^I' and marking
	the end of the line with '$'.

(.)	mark x								k
	Mark the specified line with x, a single lowercase letter.  If
	the abbreviation 'k' is used, there need not be any spaces
	between the command and the argument.

(.,.)	move address [flags]						m
	Reposition the specified lines after the given address.

(.,.)	number [count] [flags]						#
	Display the specified lines, preceded by their line number.

(.,.)	print [count] [flags]						p
	Display the specified lines.

(.)	put [buffer]							pu
	Copy lines from the secondary buffer, or from the default
	buffer if none is given, after the specified line.

	quit								q
	Quit this editing session.

	quit!								q!
	Quit this editing session, even if the main buffer has been
	modified.

(.)	read [file]							r
	Place a copy of the text in [file] after the specified line.

	set [parameter]							se
	Set without argument shows the current values of the editor
	variables.  Variables are numeric or toggles.  Toggles can be
	turned on with 'set option' and turned off with 'set nooption'.
	Numeric variables can be given a value with 'set numeric=value'.
	The following variables exist:

	    NAME	ABBREV	DEFAULT	MEANING

	    ignorecase	ic	noic	ignore case in searches.
	    shiftwidth	sw	4	affects the '&lt;', '&gt;' and 'I'
					commands.
	    window	wi	20	specifies the number of lines
					displayed with the z command.


(.,.)	substitute /pattern/replacement/ [g] [count] [flags]		s
	Replace &lt;pattern&gt; by &lt;replacement&gt; in the specified lines.  If
	the 'g' option is specified, repeat the substitution in each
	line until all occurrances of &lt;pattern&gt; have been replaced.
	In &lt;replacement&gt;, \x, where x is a digit in range 1-9, specifies
	the xth subexpression in &lt;pattern&gt;, which is enclosed by \( \)
	pairs in &lt;pattern&gt;.  Furthermore, '&' in &lt;replacement&gt; specifies
	the text that matched &lt;pattern&gt;, and '\n' in &lt;replacement&gt;
	specifies a newline, splitting the line in two.  If the symbols
	'&' and '\' themselves are desired in &lt;replacement&gt;, they should
	be prefixed by '\'.  All parameters are optional. 'substitute'
	by itself will repeat the previous substitution.

(.,.)	t address [flags]
	An alias for the 'copy' command.

	undo								u
	Undo the effects of the previous command on the main buffer.
	'edit' and 'yank' commands can not be undone, and 'global'
	commands are undone as a whole.

(1,$)	v /pattern/ [command]
	An alias for the 'global!' command.

(1,$)	write [file]							w
	Write the specified lines to [file], or to the current file if
	no argument is specified.

(1,$)	write! [file]							w!
	Write the specified lines to [file], even if some error
	occurred that prevented the main buffer from containing an exact
	image of the file that is being edited.

(1,$)	write &gt;&gt; [file]							w&gt;&gt;
	This variant of write appends to a file, instead of overwriting
	it.

(1,$)	wq [file]
	Write the main buffer to the current file, and quit this
	editing session.

(1,$)	wq! [file]
	Write the main buffer to the current file and quit this editing
	session, even if some error occurred that prevented the main
	buffer from containing an exact image of the file that is being
	edited.

	xit [file]							x
	Write the main buffer to the current file if it was modified,
	and quit this editing session.

(.,.)	yank [buffer] [count] [flags]					y
	Copy the specified lines to the secondary buffer given in the
	argument, or just to the default buffer if no argument is given.

(.+1)	z [mode] [flags]
	Show a page of lines, starting with the specified line.  The
	number of lines displayed is determined by the value of the
	'window' variable, which can be changed by the 'set' command.
	[mode] can be one of the following:

	    +	show specified line at top of page (default)
	    .	show specified line in middle of page
	    -	show specified line at bottom of page


(.,.)	&lt; [count] [flags]
	Leftshift the specified lines the number of spaces given by the
	'shiftwidth' variable, which can be changed by the 'set' command.

(.,.)	&gt; [count] [flags]
	Rightshift the specified lines the number of spaces given by the
	'shiftwidth' variable, which can be changed by the 'set' command.

($)	=
	Show the specified line number.

(1,$)	I [flags]
	Indent the specified lines, under the assumption that they are
	LPC code.  The number of spaces used for indentation is given by
	the 'shiftwidth' variable, which can be changed by the 'set'
	command.
</pre>
