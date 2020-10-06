# Template for CodeRefinery workshop webpages

This repository is a template to set up webpages for CodeRefinery workshops.

To use it, follow these instructions:
- Click the green "Use this template" button.
- Select owner of the new repository and repository name. The name should be
  "year-month-date-place", e.g. "2019-10-16-stockholm".
- Click "Create repository from template"
- You will now be redirected to the new repository.

Adjust these files:
- `title.md`
- `left-column.md`
- `right-column.md`

### Schedule planning

- **Host:** Manage zoom meeting, breakout rooms, timekeeping and breaks, zoom chat, general attendee communication.  
- **Hackmd:** watches hackmd, answers questions, organizes it, brings questions up in main lecture.  
- **Expert helpers:** Reserve instructors who can help with difficult problems, especially configuration problems at the very beginning of each day.  Optional.  
- **Helper:** breakout room helper, listed at end (not per day) since they are usually expected to be a helper every day. 
- **(name)** in parentheses: "I offer to do it but I am happy if someone replaces me here."

Overlapping roles are allowed when you think it's reasonable!


<table>
<tr>
  <th>Day</th>
         <th>Topics+Instructors</th>
         <th>Host</th>
         <th>Hackmd</th>
         <th>Experts helpers</th>
</tr>
<tr>
  <th>12.nov (Thu) 13-14 CEST</th>
         <td>
		     Installation help
	     </td>
         <td></td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>13.nov (Fri) 13-14 CEST</th>
         <td>
		     Installation help
	     </td>
         <td></td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>17.nov (Tue)</th>
         <td>
		     intro: TBA<br>
		     git-intro <br>
		 	<a href="https://coderefinery.github.io/git-intro/01-motivation/">motivation</a>: TBA<br>
		     	<a href="https://coderefinery.github.io/git-intro/04-staging-area/">staging</a>, <a href="https://coderefinery.github.io/git-intro/05-undoing/">undoing</a>: TBA<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>18.nov (Wed)</th>
         <td>
		     git-intro<br> 
		 	<a href="https://coderefinery.github.io/git-intro/06-branches/">branches and merging</a>: TBA<br>
		     	<a href="https://coderefinery.github.io/git-intro/08-conflicts/">conflict resolution</a>: TBA<br>
			<a href="https://coderefinery.github.io/git-intro/09-remotes/">sharing repositories</a>: TBA<br>
		 	<a href="https://coderefinery.github.io/git-intro/10-archaeology/">history inspection</a>: TBA<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>19.oct (The)</th>
         <td>
		     git-collab<br>
		 	<a href="https://coderefinery.github.io/git-collaborative/01-remotes/">sharing repos</a> and <a href="https://coderefinery.github.io/git-collaborative/02-centralized/">centralized workflow</a>: TBA<br>
		 <a href="https://coderefinery.github.io/git-collaborative/03-distributed/">forking</a> and <a href="https://coderefinery.github.io/git-collaborative/04-contributing/">contribution to others</a>: TBA<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>24.nov (Tue)</th>
         <td>
		     <a href="https://github.com/coderefinery/workshop-intro/blob/master/video.md">intro</a>: TBA<br>
		     	<a href="https://coderefinery.github.io/reproducible-research/">reproducible research</a>: TBA<br>
		     	<a href="https://cicero.xyz/v3/remark/0.14.0/github.com/coderefinery/social-coding/master/talk.md">social coding</a>: Annika<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>25.nov (Wed)</th>
         <td>
		    <a href="https://coderefinery.github.io/documentation/">documentation</a>: TBA<br>
		    <a href="https://coderefinery.github.io/jupyter/">jupyter</a>: TBA<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
<tr>
  <th>26.nov (Thu)</th>
         <td>
		     <a href="https://coderefinery.github.io/testing/">testing</a>: TBA<br>
		     <a href="https://github.com/coderefinery/modular-type-along">modular code development</a>: TBA<br>
		 <a href="https://github.com/coderefinery/workshop-outro/blob/master/README.md">outro</a>: TBA<br>
	     </td>
         <td>Naoe</td><!--host-->
         <td></td><!--hackmd-->
         <td></td><!--expert helpers-->
</tr>
</table>

Expert helpers:
- Stefan
- Juho
- Max

Helpers: 
- name, 
- name.  (note: for privacy, helpers do not need to be
tracked here)



### Changing the status of the registration button

Registration is not yet open:
```html
<a class="btn btn-info disabled" href="#" data-mode="1" target="_blank">Registration will open soon</a>
```

Registration is open (adjust the `href`):
```html
<a class="btn btn-success" href="#" data-mode="1" target="_blank">Register here</a>
```

Registration is closed:
```html
<a class="btn btn-danger disabled" href="#" data-mode="1" target="_blank">Registration is closed</a>
```
