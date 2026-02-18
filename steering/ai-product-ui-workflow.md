# AI Product UI Workflow

## When to Use This Workflow

Activate when user:
- Designs AI-powered product interfaces
- Creates chat-based AI UX
- Implements prompt engineering UI
- Designs AI response presentation
- Plans AI feedback mechanisms
- Creates AI model selection interfaces

---

## Production-Grade AI Product UI Design

### Phase 1: Chat Interface Architecture

**Modern AI Chat Layout:**

```
┌─────────────────────────────────────────────────────────┐
│ Chat Header                                             │
│ [Model Selector] [Settings] [History] [Share]          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ Chat Messages Area (Scrollable)                        │
│                                                         │
│ ┌─────────────────────────────────────────────────┐   │
│ │ User Message                                    │   │
│ │ "Explain quantum computing"                     │   │
│ └─────────────────────────────────────────────────┘   │
│                                                         │
│ ┌─────────────────────────────────────────────────┐   │
│ │ AI Response                                     │   │
│ │ [Streaming text with cursor...]                │   │
│ │                                                 │   │
│ │ [Copy] [👍] [👎] [Regenerate] [Continue]       │   │
│ └─────────────────────────────────────────────────┘   │
│                                                         │
├─────────────────────────────────────────────────────────┤
│ Prompt Input Area                                      │
│ ┌─────────────────────────────────────────────────┐   │
│ │ Type your message...                            │   │
│ │ [Attach] [Voice] [Send]                         │   │
│ └─────────────────────────────────────────────────┘   │
│ [Suggestion 1] [Suggestion 2] [Suggestion 3]           │
└─────────────────────────────────────────────────────────┘
```

---

### Phase 2: Streaming Response UX

**Token-by-Token Streaming:**

```tsx
<AIMessage streaming={isStreaming}>
  <MessageHeader>
    <AIAvatar>
      <SparklesIcon />
    </AIAvatar>
    <MessageMeta>
      <ModelBadge>GPT-4</ModelBadge>
      <Timestamp>Just now</Timestamp>
    </MessageMeta>
  </MessageHeader>

  <MessageContent>
    <StreamingText>
      {streamedTokens}
      {isStreaming && <StreamingCursor className="animate-pulse" />}
    </StreamingText>
    
    {isStreaming && (
      <StreamingProgress>
        <ProgressBar value={tokensGenerated} max={estimatedTokens} />
        <ProgressLabel>
          {tokensGenerated} / ~{estimatedTokens} tokens
        </ProgressLabel>
      </StreamingProgress>
    )}
  </MessageContent>

  {!isStreaming && (
    <MessageActions>
      <ActionButton icon={Copy} tooltip="Copy response">
        Copy
      </ActionButton>
      <ActionButton icon={ThumbsUp} tooltip="Good response">
        Good
      </ActionButton>
      <ActionButton icon={ThumbsDown} tooltip="Bad response">
        Bad
      </ActionButton>
      <ActionButton icon={RefreshCw} tooltip="Regenerate">
        Regenerate
      </ActionButton>
      <ActionButton icon={MessageSquare} tooltip="Continue">
        Continue
      </ActionButton>
    </MessageActions>
  )}
</AIMessage>
```

**Streaming Performance:**

```typescript
// Optimized streaming implementation
function useStreamingResponse() {
  const [tokens, setTokens] = useState<string[]>([]);
  const [isStreaming, setIsStreaming] = useState(false);

  const streamResponse = async (prompt: string) => {
    setIsStreaming(true);
    setTokens([]);

    const response = await fetch('/api/chat', {
      method: 'POST',
      body: JSON.stringify({ prompt }),
    });

    const reader = response.body?.getReader();
    const decoder = new TextDecoder();

    while (true) {
      const { done, value } = await reader!.read();
      if (done) break;

      const chunk = decoder.decode(value);
      const newTokens = chunk.split('');

      // Batch updates for performance
      setTokens(prev => [...prev, ...newTokens]);
    }

    setIsStreaming(false);
  };

  return { tokens: tokens.join(''), isStreaming, streamResponse };
}
```

---

### Phase 3: Prompt Engineering UX

**Smart Prompt Input:**

```tsx
<PromptInput>
  <InputContainer>
    <TextArea
      value={prompt}
      onChange={handleChange}
      placeholder="Ask me anything..."
      rows={1}
      autoResize
      maxRows={10}
      onKeyDown={handleKeyDown} // Cmd+Enter to send
    />
    
    {/* Character/Token Counter */}
    <InputMeta>
      <TokenCounter>
        {estimateTokens(prompt)} tokens
        {estimateTokens(prompt) > 4000 && (
          <WarningBadge>Too long</WarningBadge>
        )}
      </TokenCounter>
    </InputMeta>
  </InputContainer>

  <InputActions>
    <ActionButton icon={Paperclip} tooltip="Attach file">
      Attach
    </ActionButton>
    <ActionButton icon={Mic} tooltip="Voice input">
      Voice
    </ActionButton>
    <ActionButton 
      icon={Send} 
      variant="primary"
      disabled={!prompt.trim() || isStreaming}
      onClick={handleSend}
    >
      Send
    </ActionButton>
  </InputActions>

  {/* Smart Suggestions */}
  {showSuggestions && (
    <SuggestionChips>
      <Chip onClick={() => setPrompt('Explain this concept simply')}>
        Explain simply
      </Chip>
      <Chip onClick={() => setPrompt('Give me examples')}>
        Give examples
      </Chip>
      <Chip onClick={() => setPrompt('Make it more detailed')}>
        More details
      </Chip>
      <Chip onClick={() => setPrompt('Summarize this')}>
        Summarize
      </Chip>
    </SuggestionChips>
  )}
</PromptInput>
```

**Prompt Templates:**

```tsx
<PromptTemplates>
  <TemplateCategory>
    <CategoryTitle>Writing</CategoryTitle>
    <TemplateGrid>
      <TemplateCard onClick={() => applyTemplate('blog-post')}>
        <TemplateIcon>✍️</TemplateIcon>
        <TemplateName>Blog Post</TemplateName>
        <TemplateDescription>
          Write a blog post about [topic]
        </TemplateDescription>
      </TemplateCard>
      
      <TemplateCard onClick={() => applyTemplate('email')}>
        <TemplateIcon>📧</TemplateIcon>
        <TemplateName>Email</TemplateName>
        <TemplateDescription>
          Draft a professional email
        </TemplateDescription>
      </TemplateCard>
    </TemplateGrid>
  </TemplateCategory>

  <TemplateCategory>
    <CategoryTitle>Code</CategoryTitle>
    <TemplateGrid>
      <TemplateCard onClick={() => applyTemplate('debug')}>
        <TemplateIcon>🐛</TemplateIcon>
        <TemplateName>Debug Code</TemplateName>
        <TemplateDescription>
          Help me debug this code
        </TemplateDescription>
      </TemplateCard>
      
      <TemplateCard onClick={() => applyTemplate('explain')}>
        <TemplateIcon>💡</TemplateIcon>
        <TemplateName>Explain Code</TemplateName>
        <TemplateDescription>
          Explain how this code works
        </TemplateDescription>
      </TemplateCard>
    </TemplateGrid>
  </TemplateCategory>
</PromptTemplates>
```

---

### Phase 4: AI Response Presentation

**Markdown Rendering:**

```tsx
<AIResponse>
  <ResponseContent>
    <MarkdownRenderer
      content={aiResponse}
      components={{
        // Custom code block with syntax highlighting
        code: ({ node, inline, className, children, ...props }) => {
          const match = /language-(\w+)/.exec(className || '');
          return !inline && match ? (
            <CodeBlock language={match[1]}>
              <CodeHeader>
                <LanguageBadge>{match[1]}</LanguageBadge>
                <CopyButton code={String(children)} />
              </CodeHeader>
              <SyntaxHighlighter language={match[1]}>
                {String(children)}
              </SyntaxHighlighter>
            </CodeBlock>
          ) : (
            <code className={className} {...props}>
              {children}
            </code>
          );
        },
        
        // Custom table styling
        table: ({ children }) => (
          <TableContainer>
            <Table>{children}</Table>
          </TableContainer>
        ),
        
        // Custom link handling
        a: ({ href, children }) => (
          <ExternalLink href={href} target="_blank" rel="noopener">
            {children}
            <ExternalLinkIcon />
          </ExternalLink>
        ),
      }}
    />
  </ResponseContent>

  {/* Source Citations */}
  {sources && sources.length > 0 && (
    <ResponseSources>
      <SourcesTitle>Sources</SourcesTitle>
      <SourcesList>
        {sources.map((source, index) => (
          <SourceItem key={index}>
            <SourceNumber>[{index + 1}]</SourceNumber>
            <SourceLink href={source.url}>
              {source.title}
            </SourceLink>
          </SourceItem>
        ))}
      </SourcesList>
    </ResponseSources>
  )}
</AIResponse>
```

---

### Phase 5: Confidence & Trust Indicators

**Model Confidence Display:**

```tsx
<AIResponse>
  <ResponseContent>{content}</ResponseContent>

  {/* Confidence Indicator */}
  <ConfidenceSection>
    <ConfidenceLabel>Response Confidence</ConfidenceLabel>
    <ConfidenceBar>
      <ConfidenceFill 
        level={confidence}
        style={{ width: `${confidence * 100}%` }}
      />
    </ConfidenceBar>
    <ConfidenceText>
      {confidence > 0.8 ? (
        <HighConfidence>
          <CheckCircle /> High confidence
        </HighConfidence>
      ) : confidence > 0.5 ? (
        <MediumConfidence>
          <AlertCircle /> Medium confidence
        </MediumConfidence>
      ) : (
        <LowConfidence>
          <AlertTriangle /> Low confidence - verify information
        </LowConfidence>
      )}
    </ConfidenceText>
  </ConfidenceSection>

  {/* Uncertainty Warning */}
  {confidence < 0.5 && (
    <WarningBanner variant="warning">
      <WarningIcon />
      <WarningContent>
        <WarningTitle>Uncertain Response</WarningTitle>
        <WarningMessage>
          This response may contain inaccuracies. Please verify with
          authoritative sources before using this information.
        </WarningMessage>
      </WarningContent>
    </WarningBanner>
  )}

  {/* Fact-Check Suggestions */}
  {confidence < 0.7 && factCheckUrls && (
    <FactCheckSection>
      <FactCheckTitle>Verify with these sources:</FactCheckTitle>
      <FactCheckLinks>
        {factCheckUrls.map((url, index) => (
          <FactCheckLink key={index} href={url} target="_blank">
            {getDomain(url)}
          </FactCheckLink>
        ))}
      </FactCheckLinks>
    </FactCheckSection>
  )}
</AIResponse>
```

---

### Phase 6: Multi-Turn Refinement

**Conversation Refinement Flow:**

```tsx
<ConversationThread>
  {/* Initial Prompt */}
  <UserMessage>
    <MessageContent>
      Write a blog post about AI ethics
    </MessageContent>
  </UserMessage>

  {/* First Response */}
  <AIMessage id="response-1">
    <MessageContent>{response1}</MessageContent>
    <MessageActions>
      <RefineButton onClick={() => showRefinementOptions('response-1')}>
        <Edit /> Refine
      </RefineButton>
    </MessageActions>
  </AIMessage>

  {/* Refinement Prompt */}
  <RefinementMessage>
    <RefinementBadge>Refinement</RefinementBadge>
    <MessageContent>
      Make it more technical and add examples
    </MessageContent>
  </RefinementMessage>

  {/* Improved Response */}
  <AIMessage id="response-2" improved>
    <ImprovedBadge>
      <Sparkles /> Improved Response
    </ImprovedBadge>
    <MessageContent>{response2}</MessageContent>
    <MessageActions>
      <CompareButton onClick={() => compareVersions('response-1', 'response-2')}>
        <GitCompare /> Compare Versions
      </CompareButton>
    </MessageActions>
  </AIMessage>
</ConversationThread>

{/* Version Comparison Modal */}
{showComparison && (
  <ComparisonModal>
    <ComparisonHeader>
      <ComparisonTitle>Response Comparison</ComparisonTitle>
      <CloseButton onClick={closeComparison} />
    </ComparisonHeader>
    
    <ComparisonContent>
      <ComparisonColumn>
        <ColumnHeader>Original</ColumnHeader>
        <ColumnContent>{response1}</ColumnContent>
      </ComparisonColumn>
      
      <ComparisonColumn>
        <ColumnHeader>Improved</ColumnHeader>
        <ColumnContent>{response2}</ColumnContent>
        <ImprovementBadges>
          <Badge variant="success">More detailed</Badge>
          <Badge variant="success">Better examples</Badge>
        </ImprovementBadges>
      </ComparisonColumn>
    </ComparisonContent>
  </ComparisonModal>
)}
```

---

### Phase 7: Editable AI Responses

**Inline Editing:**

```tsx
<AIResponse>
  <ResponseHeader>
    <EditToggle
      checked={isEditing}
      onChange={setIsEditing}
      label="Edit mode"
    />
  </ResponseHeader>

  <ResponseContent
    contentEditable={isEditing}
    suppressContentEditableWarning
    onBlur={handleEdit}
    className={isEditing ? 'editing' : ''}
  >
    {content}
  </ResponseContent>

  {isEditing && (
    <EditingToolbar>
      <ToolbarButton onClick={formatBold}>
        <Bold /> Bold
      </ToolbarButton>
      <ToolbarButton onClick={formatItalic}>
        <Italic /> Italic
      </ToolbarButton>
      <ToolbarButton onClick={insertLink}>
        <Link /> Link
      </ToolbarButton>
      <ToolbarDivider />
      <ToolbarButton onClick={saveEdit} variant="primary">
        <Save /> Save Changes
      </ToolbarButton>
      <ToolbarButton onClick={cancelEdit} variant="outline">
        <X /> Cancel
      </ToolbarButton>
    </EditingToolbar>
  )}

  {/* Edit History */}
  {editHistory.length > 0 && (
    <EditHistory>
      <HistoryTitle>Edit History</HistoryTitle>
      <HistoryList>
        {editHistory.map((edit, index) => (
          <HistoryItem key={index}>
            <HistoryTimestamp>{edit.timestamp}</HistoryTimestamp>
            <HistoryAction>{edit.action}</HistoryAction>
            <HistoryRevert onClick={() => revertToVersion(index)}>
              Revert
            </HistoryRevert>
          </HistoryItem>
        ))}
      </HistoryList>
    </EditHistory>
  )}
</AIResponse>
```

---

### Phase 8: Safety & Content Moderation

**Content Filtering UI:**

```tsx
{/* Content Moderation Warning */}
{isContentFlagged && (
  <ContentModerationBanner variant="error">
    <BannerIcon>
      <ShieldAlert />
    </BannerIcon>
    <BannerContent>
      <BannerTitle>Content Filtered</BannerTitle>
      <BannerMessage>
        This response was filtered due to our content policy.
        The AI detected potentially harmful or inappropriate content.
      </BannerMessage>
      <BannerDetails>
        <DetailItem>
          <DetailLabel>Reason:</DetailLabel>
          <DetailValue>{moderationReason}</DetailValue>
        </DetailItem>
        <DetailItem>
          <DetailLabel>Category:</DetailLabel>
          <DetailValue>{moderationCategory}</DetailValue>
        </DetailItem>
      </BannerDetails>
    </BannerContent>
    <BannerActions>
      <Button variant="outline" onClick={reportFalsePositive}>
        Report False Positive
      </Button>
      <Button variant="primary" onClick={tryDifferentPrompt}>
        Try Different Prompt
      </Button>
    </BannerActions>
  </ContentModerationBanner>
)}

{/* Rate Limit */}
{isRateLimited && (
  <RateLimitBanner variant="warning">
    <BannerIcon>
      <Clock />
    </BannerIcon>
    <BannerContent>
      <BannerTitle>Rate Limit Reached</BannerTitle>
      <BannerMessage>
        You've reached your usage limit for this hour.
      </BannerMessage>
      <Countdown>
        <CountdownLabel>Try again in:</CountdownLabel>
        <CountdownTimer>{formatTime(timeRemaining)}</CountdownTimer>
      </Countdown>
    </BannerContent>
    <BannerActions>
      <Button variant="primary" onClick={upgradePlan}>
        Upgrade Plan
      </Button>
    </BannerActions>
  </RateLimitBanner>
)}

{/* API Error */}
{hasError && (
  <ErrorState>
    <ErrorIcon>
      <AlertCircle size={48} />
    </ErrorIcon>
    <ErrorTitle>Something went wrong</ErrorTitle>
    <ErrorMessage>{errorMessage}</ErrorMessage>
    <ErrorCode>Error Code: {errorCode}</ErrorCode>
    <ErrorActions>
      <Button variant="primary" onClick={retry}>
        <RefreshCw /> Retry
      </Button>
      <Button variant="outline" onClick={contactSupport}>
        <MessageCircle /> Contact Support
      </Button>
    </ErrorActions>
  </ErrorState>
)}
```

---

### Phase 9: Model Selection & Settings

**Model Selector:**

```tsx
<ModelSelector>
  <SelectorTrigger>
    <CurrentModel>
      <ModelIcon>{currentModel.icon}</ModelIcon>
      <ModelInfo>
        <ModelName>{currentModel.name}</ModelName>
        <ModelDescription>{currentModel.description}</ModelDescription>
      </ModelInfo>
    </CurrentModel>
    <ChevronDown />
  </SelectorTrigger>

  <SelectorDropdown>
    <ModelOption
      selected={currentModel.id === 'gpt-4'}
      onClick={() => selectModel('gpt-4')}
    >
      <ModelIcon>🧠</ModelIcon>
      <ModelDetails>
        <ModelName>GPT-4</ModelName>
        <ModelDescription>Most capable, slower</ModelDescription>
        <ModelBadges>
          <Badge>128K context</Badge>
          <Badge variant="success">Best quality</Badge>
        </ModelBadges>
      </ModelDetails>
      <ModelCost>$0.03/1K tokens</ModelCost>
    </ModelOption>

    <ModelOption
      selected={currentModel.id === 'gpt-3.5-turbo'}
      onClick={() => selectModel('gpt-3.5-turbo')}
    >
      <ModelIcon>⚡</ModelIcon>
      <ModelDetails>
        <ModelName>GPT-3.5 Turbo</ModelName>
        <ModelDescription>Fast and efficient</ModelDescription>
        <ModelBadges>
          <Badge>16K context</Badge>
          <Badge variant="info">Fastest</Badge>
        </ModelBadges>
      </ModelDetails>
      <ModelCost>$0.001/1K tokens</ModelCost>
    </ModelOption>

    <ModelOption
      selected={currentModel.id === 'claude-3'}
      onClick={() => selectModel('claude-3')}
    >
      <ModelIcon>🎭</ModelIcon>
      <ModelDetails>
        <ModelName>Claude 3</ModelName>
        <ModelDescription>Great for analysis</ModelDescription>
        <ModelBadges>
          <Badge>200K context</Badge>
          <Badge variant="warning">Beta</Badge>
        </ModelBadges>
      </ModelDetails>
      <ModelCost>$0.015/1K tokens</ModelCost>
    </ModelOption>
  </SelectorDropdown>
</ModelSelector>
```

**Advanced Settings:**

```tsx
<SettingsPanel>
  <SettingsSection>
    <SectionTitle>Response Settings</SectionTitle>
    
    <SettingItem>
      <SettingLabel>
        Temperature
        <Tooltip>Controls randomness. Higher = more creative</Tooltip>
      </SettingLabel>
      <Slider
        value={temperature}
        onChange={setTemperature}
        min={0}
        max={2}
        step={0.1}
        marks={[
          { value: 0, label: 'Precise' },
          { value: 1, label: 'Balanced' },
          { value: 2, label: 'Creative' },
        ]}
      />
      <SettingValue>{temperature}</SettingValue>
    </SettingItem>

    <SettingItem>
      <SettingLabel>
        Max Length
        <Tooltip>Maximum response length in tokens</Tooltip>
      </SettingLabel>
      <Select value={maxTokens} onChange={setMaxTokens}>
        <SelectOption value={500}>Short (500 tokens)</SelectOption>
        <SelectOption value={1000}>Medium (1000 tokens)</SelectOption>
        <SelectOption value={2000}>Long (2000 tokens)</SelectOption>
        <SelectOption value={4000}>Very Long (4000 tokens)</SelectOption>
      </Select>
    </SettingItem>

    <SettingItem>
      <SettingLabel>Response Style</SettingLabel>
      <RadioGroup value={style} onChange={setStyle}>
        <Radio value="concise">Concise</Radio>
        <Radio value="detailed">Detailed</Radio>
        <Radio value="technical">Technical</Radio>
        <Radio value="simple">Simple</Radio>
      </RadioGroup>
    </SettingItem>
  </SettingsSection>

  <SettingsSection>
    <SectionTitle>Safety Settings</SectionTitle>
    
    <SettingItem>
      <SettingLabel>Content Filtering</SettingLabel>
      <Toggle
        checked={contentFiltering}
        onChange={setContentFiltering}
        label="Enable content moderation"
      />
    </SettingItem>

    <SettingItem>
      <SettingLabel>Fact Checking</SettingLabel>
      <Toggle
        checked={factChecking}
        onChange={setFactChecking}
        label="Show confidence indicators"
      />
    </SettingItem>
  </SettingsSection>
</SettingsPanel>
```

---

## Behavioral Psychology for AI UX

### Trust Building:
- **Transparency**: Always show which model is responding
- **Confidence**: Display uncertainty when appropriate
- **Sources**: Cite sources for factual claims
- **Editability**: Allow users to correct AI responses
- **Feedback**: Enable thumbs up/down for training

### Cognitive Load Reduction:
- **Streaming**: Show progress, don't make users wait
- **Suggestions**: Provide prompt templates
- **History**: Easy access to past conversations
- **Shortcuts**: Keyboard shortcuts for power users

### Error Prevention:
- **Token Counter**: Warn before hitting limits
- **Confirmation**: Confirm destructive actions
- **Auto-save**: Save conversations automatically
- **Undo**: Allow reverting to previous versions

---

## Performance Optimization

```typescript
// Virtualize long conversations
<VirtualizedChatList
  messages={messages}
  height={600}
  itemSize={100}
  overscan={5}
/>

// Lazy load message history
const { data, fetchNextPage } = useInfiniteQuery({
  queryKey: ['messages'],
  queryFn: ({ pageParam = 0 }) => fetchMessages(pageParam),
  getNextPageParam: (lastPage) => lastPage.nextCursor,
});

// Debounce typing indicators
const debouncedTyping = useDebouncedCallback(
  () => sendTypingIndicator(),
  1000
);
```

---

## Production Checklist

- [ ] Streaming responses implemented
- [ ] Token counter visible
- [ ] Confidence indicators shown
- [ ] Content moderation enabled
- [ ] Rate limiting handled gracefully
- [ ] Error states designed
- [ ] Keyboard shortcuts work
- [ ] Mobile responsive
- [ ] Accessibility compliant
- [ ] Performance optimized (virtualization)
- [ ] Edit history tracked
- [ ] Sources cited
- [ ] Model selection clear
- [ ] Settings accessible
- [ ] Feedback mechanisms in place

---

This workflow ensures production-grade AI product UI with trust, transparency, and excellent UX.
