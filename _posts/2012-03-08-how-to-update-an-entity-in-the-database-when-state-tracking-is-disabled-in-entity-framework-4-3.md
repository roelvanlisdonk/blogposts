---
ID: 2547
post_title: >
  How to update an entity in the database,
  when state tracking is disabled in
  Entity Framework 4.3
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/08/how-to-update-an-entity-in-the-database-when-state-tracking-is-disabled-in-entity-framework-4-3/
published: true
post_date: 2012-03-08 10:51:09
---
<p>When you disable state tracking in Entity Framework 4.3, for performance improvements (and you know what you’re doing <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Winking smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/wlEmoticon-winkingsmile.png" />), by setting: DbContext.Configuration.AutoDetectChangesEnabled = <span style="color: blue">false </span>, then you are responsible for your own state tracking on entities.</p>  <p>&#160;</p>  <p><strong>The process of updating an entity, involves 3 steps:</strong></p>  <p>1. Setting the EntityState to Modified.</p>  <p>2. Save changes to database.</p>  <p>3. Setting the EntityState to Unchanged.</p>  <p>&#160;</p>  <p><strong>Code</strong></p>  <pre class="code"><span style="color: green">// Set entity to modified, so the entity will be updated in the database.
</span>_dbContext.Entry(imageInfo).State = System.Data.<span style="color: #2b91af">EntityState</span>.Modified;

<span style="color: green">// Save changes to database.
</span>_dbContext.SaveChanges();

<span style="color: green">// Set entity to unchanged, so the entity will be not be updated in future calls to _dbContext.SaveChanges().
</span>_dbContext.Entry(imageInfo).State = System.Data.<span style="color: #2b91af">EntityState</span>.Unchanged;    </pre>


<p><strong>Notes</strong></p>

<p>1. Where _dbConext is an instance of the DbContext class.</p>

<p>2. If you don’t set the Entity.State to Modified, no changes will be persisted to the database.</p>

<p>3. If you don’t set the Entity.State to Unchanged after SaveChanges(), future calls to SaveChanges() will repeat the update for this entity. </p>