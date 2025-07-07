# Voice Interface Design Patterns

## Conversation Design
- Use the 6-building-block framework for all voice agents
- Design natural conversation flows with proper turn-taking
- Implement context preservation across conversation turns
- Handle interruptions and conversation recovery gracefully

## Prompt Engineering
- Create distinct personalities optimized for voice delivery
- Use strategic pauses and emphasis for TTS optimization
- Adapt language complexity based on user expertise
- Include natural speech markers and filler words

## Audio Quality
- Maintain minimum 16kHz sample rate for speech recognition
- Implement echo cancellation and noise suppression
- Use adaptive bitrate for varying network conditions
- Provide graceful degradation for poor audio quality

## Error Handling
- Implement fallback to text-based interaction
- Provide clear audio quality feedback to users
- Handle network failures with automatic reconnection
- Preserve conversation context during technical issues