<%*
// Get citekey from 'citekey' property, or alias starting with '@' or file name
const citekey = tp.frontmatter?.citekey || tp.frontmatter.aliases?.find(alias => alias.startsWith('@')) || tp.file.title;
// Get the library ID from the properties. Fall back to "My Library" (1), if the library ID is not accessible
const libraryID = tp.frontmatter.libraryID || 1;
// Run the import
app.plugins.getPlugin('obsidian-zotero-desktop-connector').runImport('Paper Note', citekey, libraryID); ;
%>
