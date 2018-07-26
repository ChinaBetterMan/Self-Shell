# Self-Shell
Self-Shell Script （Shell脚本仓库）
 <div id="readme" class="readme blob instapaper_body">
<p>William在Linux运维工作中使用的shell脚本整理版</p>

<h2><a id="user-content-git远程操作详解" class="anchor" aria-hidden="true" href="#git远程操作详解"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Git远程操作详解</h2>
<h3><a id="user-content-一git-clone" class="anchor" aria-hidden="true" href="#一git-clone"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>一、git clone</h3>
<p>远程操作的第一步，通常是从远程主机克隆一个版本库，这时就要用到git clone命令。</p>
<pre><code>$ git clone &lt;版本库的网址&gt;

</code></pre>
<p>比如，克隆jQuery的版本库。</p>
<pre><code>$ git clone https://github.com/jquery/jquery.git

</code></pre>
<p>该命令会在本地主机生成一个目录，与远程主机的版本库同名。如果要指定不同的目录名，可以将目录名作为git clone命令的第二个参数。</p>
<pre><code>$ git clone &lt;版本库的网址&gt; &lt;本地目录名&gt;

</code></pre>
<p>git clone支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子。</p>
<pre><code>$ git clone http[s]://example.com/path/to/repo.git/
$ git clone ssh://example.com/path/to/repo.git/
$ git clone git://example.com/path/to/repo.git/
$ git clone /opt/git/project.git 
$ git clone file:///opt/git/project.git
$ git clone ftp[s]://example.com/path/to/repo.git/
$ git clone rsync://example.com/path/to/repo.git/

</code></pre>
<p>SSH协议还有另一种写法。</p>
<pre><code>$ git clone [user@]example.com:path/to/repo.git/

</code></pre>
<p>通常来说，Git协议下载速度最快，SSH协议用于需要用户认证的场合。各种协议优劣的详细讨论请参考<a href="https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols" rel="nofollow">官方文档</a></p>
<h3><a id="user-content-二git-remote" class="anchor" aria-hidden="true" href="#二git-remote"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>二、git remote</h3>
<p>为了便于管理，Git要求每个远程主机都必须指定一个主机名。git remote命令就用于管理主机名。
不带选项的时候，git remote命令列出所有远程主机。</p>
<pre><code>$ git remote
origin
</code></pre>
<p>使用-v选项，可以参看远程主机的网址。</p>
<pre><code>$ git remote -v
origin  git@github.com:jquery/jquery.git (fetch)
origin  git@github.com:jquery/jquery.git (push)
</code></pre>
<p>上面命令表示，当前只有一台远程主机，叫做origin，以及它的网址。
克隆版本库的时候，所使用的远程主机自动被Git命名为origin。如果想用其他的主机名，需要用git clone命令的-o选项指定。</p>
<pre><code>$ git clone -o jQuery https://github.com/jquery/jquery.git
$ git remote
jQuery
</code></pre>
<p>上面命令表示，克隆的时候，指定远程主机叫做jQuery。
git remote show命令加上主机名，可以查看该主机的详细信息。</p>
<pre><code>$ git remote show &lt;主机名&gt;
git remote add命令用于添加远程主机。

$ git remote add &lt;主机名&gt; &lt;网址&gt;
git remote rm命令用于删除远程主机。

$ git remote rm &lt;主机名&gt;
git remote rename命令用于远程主机的改名。

$ git remote rename &lt;原主机名&gt; &lt;新主机名&gt;
</code></pre>
<h3><a id="user-content-三git-fetch" class="anchor" aria-hidden="true" href="#三git-fetch"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>三、git fetch</h3>
<p>一旦远程主机的版本库有了更新（Git术语叫做commit），需要将这些更新取回本地，这时就要用到git fetch命令。</p>
<pre><code>$ git fetch &lt;远程主机名&gt;
</code></pre>
<p>上面命令将某个远程主机的更新，全部取回本地。
git fetch命令通常用来查看其他人的进程，因为它取回的代码对你本地的开发代码没有影响。
默认情况下，git fetch取回所有分支（branch）的更新。如果只想取回特定分支的更新，可以指定分支名。</p>
<pre><code>$ git fetch &lt;远程主机名&gt; &lt;分支名&gt;
</code></pre>
<p>比如，取回origin主机的master分支。</p>
<pre><code>$ git fetch origin master
</code></pre>
<p>所取回的更新，在本地主机上要用"远程主机名/分支名"的形式读取。比如origin主机的master，就要用origin/master读取。
git branch命令的-r选项，可以用来查看远程分支，-a选项查看所有分支。</p>
<pre><code>$ git branch -r
origin/master

$ git branch -a
* master
  remotes/origin/master
</code></pre>
<p>上面命令表示，本地主机的当前分支是master，远程分支是origin/master。
取回远程主机的更新以后，可以在它的基础上，使用git checkout命令创建一个新的分支。</p>
<pre><code>$ git checkout -b newBrach origin/master

</code></pre>
<p>上面命令表示，在origin/master的基础上，创建一个新分支。
此外，也可以使用git merge命令或者git rebase命令，在本地分支上合并远程分支。</p>
<pre><code>$ git merge origin/master
</code></pre>
<h5><a id="user-content-或者" class="anchor" aria-hidden="true" href="#或者"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>或者</h5>
<pre><code>$ git rebase origin/master
</code></pre>
<p>上面命令表示在当前分支上，合并origin/master。</p>
<h3><a id="user-content-四git-pull" class="anchor" aria-hidden="true" href="#四git-pull"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>四、git pull</h3>
<p>git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。</p>
<pre><code>$ git pull &lt;远程主机名&gt; &lt;远程分支名&gt;:&lt;本地分支名&gt;
</code></pre>
<p>比如，取回origin主机的next分支，与本地的master分支合并，需要写成下面这样。</p>
<pre><code>$ git pull origin next:master
</code></pre>
<p>如果远程分支是与当前分支合并，则冒号后面的部分可以省略。</p>
<pre><code>$ git pull origin next
</code></pre>
<p>上面命令表示，取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge。</p>
<pre><code>$ git fetch origin
$ git merge origin/next
</code></pre>
<p>在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系（tracking）。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动"追踪"origin/master分支。
Git也允许手动建立追踪关系。</p>
<pre><code>git branch --set-upstream master origin/next

</code></pre>
<p>上面命令指定master分支追踪origin/next分支。
如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。</p>
<p>$ git pull origin
上面命令表示，本地的当前分支自动与对应的origin主机"追踪分支"（remote-tracking branch）进行合并。
如果当前分支只有一个追踪分支，连远程主机名都可以省略。</p>
<pre><code>$ git pull
</code></pre>
<p>上面命令表示，当前分支自动与唯一一个追踪分支进行合并。
如果合并需要采用rebase模式，可以使用--rebase选项。</p>
<pre><code>$ git pull --rebase &lt;远程主机名&gt; &lt;远程分支名&gt;:&lt;本地分支名&gt;
</code></pre>
<p>如果远程主机删除了某个分支，默认情况下，git pull不会在拉取远程分支的时候，删除对应的本地分支。这是为了防止，由于其他人操作了远程主机，导致git pull不知不觉删除了本地分支。</p>
<p>但是，你可以改变这个行为，加上参数 -p 就会在本地删除远程已经删除的分支。</p>
<pre><code>$ git pull -p

</code></pre>
<h5><a id="user-content-等同于下面的命令" class="anchor" aria-hidden="true" href="#等同于下面的命令"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>等同于下面的命令</h5>
<pre><code>$ git fetch --prune origin 
$ git fetch -p

</code></pre>
<h3><a id="user-content-五git-push" class="anchor" aria-hidden="true" href="#五git-push"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>五、git push</h3>
<p>git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相仿。</p>
<pre><code>$ git push &lt;远程主机名&gt; &lt;本地分支名&gt;:&lt;远程分支名&gt;
</code></pre>
<p>注意，分支推送顺序的写法是&lt;来源地&gt;:&lt;目的地&gt;，所以git pull是&lt;远程分支&gt;:&lt;本地分支&gt;，而git push是&lt;本地分支&gt;:&lt;远程分支&gt;。</p>
<p>如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。</p>
<pre><code>$ git push origin master
</code></pre>
<p>上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。
如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。</p>
<pre><code>$ git push origin :master
</code></pre>
<h5><a id="user-content-等同于" class="anchor" aria-hidden="true" href="#等同于"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>等同于</h5>
<pre><code>$ git push origin --delete master
</code></pre>
<p>上面命令表示删除origin主机的master分支。
如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。</p>
<p>$ git push origin
上面命令表示，将当前分支推送到origin主机的对应分支。
如果当前分支只有一个追踪分支，那么主机名都可以省略。</p>
<pre><code>$ git push

</code></pre>
<p>如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。</p>
<pre><code>$ git push -u origin master

</code></pre>
<p>上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。</p>
<p>不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。</p>
<pre><code>$ git config --global push.default matching

</code></pre>
<h5><a id="user-content-或者-1" class="anchor" aria-hidden="true" href="#或者-1"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>或者</h5>
<pre><code>$ git config --global push.default simple

</code></pre>
<p>还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用--all选项。</p>
<pre><code>$ git push --all origin
</code></pre>
<p>上面命令表示，将所有本地分支都推送到origin主机。
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用--force选项。</p>
<pre><code>$ git push --force origin 
</code></pre>
<p>上面命令使用--force选项，结果导致远程主机上更新的版本被覆盖。除非你很确定要这样做，否则应该尽量避免使用--force选项。
最后，git push不会推送标签（tag），除非使用--tags选项。</p>
<pre><code>$ git push origin --tags
</code></pre>
